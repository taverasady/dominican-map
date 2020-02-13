<template>
  <section>
    <div v-show="isBackButtonVisible">
      <transition name="slide-fade" appear mode="out-in">
        <button
          class="button"
          id="theButton"
          v-show="isButtonVisible"
          @click="drillUpAction"
        >{{ buttonMessage ? buttonMessage : "Atras" }}</button>
      </transition>
    </div>

    <br />
    <div id="container" ref="map"></div>
  </section>
</template>
<style lang='css' src="./DominicanGeoMap.css"></style>
<script>
// import Anychart from "anychart/index.js";
import "@/assets/data/js/proj4.js";

export default {
  name: "DominicanGeoMap",
  props: {
    mapTitle: String,
    hasToolTipMessage: Boolean,
    hasToolTipMessageDetailMap: Boolean,
    mapToolTipMessage: String,
    toolTipValue: String,
    detailMapToolTip: String,
    detailMapToolTipValue: String,
    fromMainMapValue: String,
    toMainMapValue: String,
    greaterThanMainMapValue: String,
    fromToMainMapColor: String,
    greaterThanMainMapColor: String,
    fromDetailedMapValue: String,
    toDetailedMapValue: String,
    greaterThanDetailedMapValue: String,
    fromToDetailedMapColor: String,
    greaterThanDetailedMapColor: String,
    buttonMessage: String,
    isBackButtonVisible: Boolean,
    mapDataSrc: null,
    innerMapCustomData: null,
  },
  data() {
    return {
      map: null,
      drillMap: null,
      preloader: null,
      isButtonVisible: false,
      mapData: null,
      dataSet: null,
    };
  },
  mounted() {
    this.loadMap();
    document.addEventListener("keyup", evt => {
      if (evt.keyCode === 27) {
        this.drillUpAction();
      }
    });
  },
  methods: {
    drillUpAction() {
      this.isButtonVisible = false;
      this.drillMap.drillUp();
    },

    loadMap() {
      const Anychart = require("anychart/index.js");
      this.map = Anychart.map();
      this.preloader = Anychart.ui.preloader();
      this.preloader.render(this.$refs.map);
      if (this.mapDataSrc) {
        this.mapData = this.mapDataSrc;
      } else {
        this.mapData = require("@/assets/data/js/map-chart-data.json");
      }
      // sets map padding and interactivity settings
      this.map.padding([10, 10, 10, 10]);
      this.map.interactivity().selectionMode("none");

      var menu = this.map.contextMenu();
      // add item DrillUp for context menu
      menu.itemsFormatter(items => {
        var path = this.map.getDrilldownPath();

        items["drill-up"] = {
          index: 0,
          text: "Drill Up",
          action: () => {
            this.map.drillUp();
          }
        };

        path.length <= 1
          ? (items["drill-up"].enabled = false)
          : (items["drill-up"].enabled = true);

        return items;
      });
      var dataSet = Anychart.data.set(this.mapData);
      var series = this.map.choropleth(dataSet);
      this.map
        .tooltip()
        .titleFormat(`{%${this.mapTitle ? this.mapTitle : "provienceName"}}`);
      if (this.hasToolTipMessage) {
        this.map
          .tooltip()
          .format(`${this.mapToolTipMessage} {%${this.toolTipValue}}`);
      } else {
        this.map.tooltip().format(`{%value}`);
      }
      series.geoIdField("id");
      // series.colorScale(Anychart.scales.linearColor("#deebf7", "#3182bd"));
      series.colorScale(
        Anychart.scales.ordinalColor([
          {
            from: this.fromMainMapValue ? parseInt(this.fromMainMapValue) : 0,
            to: this.toMainMapValue ? parseInt(this.toMainMapValue) : 200,
            color: this.fromToMainMapColor ? this.fromToMainMapColor : "#4a89d9"
          },
          {
            greater: this.greaterThanMainMapValue
              ? parseInt(this.greaterThanMainMapValue)
              : 201,
            color: this.greaterThanMainMapColor
              ? this.greaterThanMainMapColor
              : "#d63a3a"
          }
        ])
      );
      series.labels(false);
      this.map.geoData(
        require("@/assets/data/js/republica-dominicana-geo.json")
      );
      this.map.listen("pointClick", this.onPointClickHandler);
      this.map.container(this.$refs.map);
      this.map.draw();
      const removeElements = elms => elms.forEach(el => el.remove());
      removeElements(document.querySelectorAll(".anychart-credits"));
    },
    onPointClickHandler(evt) {
      var point = evt.point;
      var stateId = point.get("id");
      if (!stateId.startsWith("DO")) {
        //logic when is a municipio
      } else {
        const Anychart = require("anychart/index.js");

        // create map fro drill down
        this.drillMap = Anychart.map();
        if (this.innerMapCustomData) {
          var result = this.innerMapCustomData.filter(x => {
            return x.provincia == stateId;
          });
          this.dataSet = Anychart.data.set(result);
        } else {
          this.dataSet = Anychart.data.set(
            require(`@/assets/data/json/provincias/${stateId}/data.json`)
          );
        }
        this.drillMap.geoIdField("id");
        var series = this.drillMap.choropleth(this.dataSet);
        series.colorScale(
          Anychart.scales.ordinalColor([
            {
              from: this.fromDetailedMapValue
                ? parseInt(this.fromDetailedMapValue)
                : 0,
              to: this.toDetailedMapValue
                ? parseInt(this.toDetailedMapValue)
                : 200,
              color: this.fromToDetailedMapColor
                ? this.fromToDetailedMapColor
                : "#4a89d9"
            },
            {
              greater: this.greaterThanDetailedMapValue
                ? parseInt(this.greaterThanDetailedMapValue)
                : 201,
              color: this.greaterThanDetailedMapColor
                ? this.greaterThanDetailedMapColor
                : "#d63a3a"
            }
          ])
        );
        series.labels(true);
        series.labels().format("{%municipioName}");
        this.drillMap.tooltip().titleFormat("{%municipioName}");

        if (this.hasToolTipMessageDetailMap) {
          this.drillMap.tooltip().format(`${this.detailMapToolTip} {%value}`);
        } else {
          this.drillMap.tooltip().format(`{%value}`);
        }

        this.drillMap
          .geoData(require(`@/assets/data/json/provincias/${stateId}/geo.json`))
          // set drill down map padding settings
          .padding([10, 10, 10, 10]);

        this.drillMap
          .title()
          .enabled(true)
          .useHtml(true)
          .padding([0, 0, 10, 0])
          .text("");

        // initiate drill down
        this.map.drillTo(stateId, this.drillMap);

        // hide preloader
        this.preloader.visible(false);
        this.isButtonVisible = true;
      }
    }
  }
};
</script> 

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html,
body,
#container {
  width: 800px;
  height: 500px;
  margin: 0;
  padding: 0;
}
</style>
