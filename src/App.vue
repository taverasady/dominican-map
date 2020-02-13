<template>
  <div id="app">
    <DominicanGeoMap
      mapTitle="provienceName"
      v-bind:hasToolTipMessage="true"
      v-bind:hasToolTipMessageDetailMap="true"
      v-bind:isBackButtonVisible="true"
      mapToolTipMessage="Total de edificaciones actuales:"
      toolTipValue="value"
      detailMapToolTip="Totales:"
      detailMapToolTipValue="value"
      fromMainMapValue="0"
      toMainMapValue="299"
      fromToMainMapColor="#2abf81"
      greaterThanMainMapValue="300"
      greaterThanMainMapColor="#c8defa"
      fromDetailedMapValue="0"
      toDetailedMapValue="200"
      fromToDetailedMapColor="#d6853a"
      greaterThanDetailedMapValue="201"
      greaterThanDetailedMapColor="#a22cd1"
      buttonMessage="Go back"
      :mapDataSrc="customData"
      :innerMapCustomData="customInnerData"
    />
  </div>
</template>

<script>
import DominicanGeoMap from "./components/DominicanGeoMap.vue";
export default {
  name: "app",
  components: {
    DominicanGeoMap
  },
  data() {
    return {
      customData: [
        { id: "DO.ST", value: "0125", provienceName: "SANTIAGO" },
        { id: "DO.SR", value: "0426", provienceName: "SANTIAGO RODRÍGUEZ" },
        { id: "DO.VA", value: "0427", provienceName: "VALVERDE" },
        { id: "DO.JU", value: "0722", provienceName: "San Juan" },
        { id: "DO.SD", value: "1032", provienceName: "SANTO DOMINGO" },
        { id: "DO.SZ", value: "0224", provienceName: "SANCHEZ RAMÍREZ" },
        { id: "DO.PM", value: "0923", provienceName: "SAN PEDRO DE MACORIS" },
        { id: "DO.MC", value: "0415", provienceName: "MONTE CRISTI" },
        { id: "DO.PP", value: "0118", provienceName: "PUERTO PLATA" },
        { id: "DO.DA", value: "0405", provienceName: "DAJABON" },
        { id: "DO.ES", value: "0109", provienceName: "ESPAILLAT" },
        { id: "DO.MM", value: "0319", provienceName: "HERMANAS MIRABAL" },
        { id: "DO.BR", value: "0603", provienceName: "BAORUCO" },
        { id: "DO.BH", value: "0604", provienceName: "BARAHONA" },
        { id: "DO.IN", value: "0610", provienceName: "Independencia" },
        { id: "DO.EP", value: "0707", provienceName: "ELÍAS PIÑA" },
        { id: "DO.PN", value: "0616", provienceName: "Pedernales" },
        { id: "DO.AZ", value: "0502", provienceName: "Azua2" },
        { id: "DO.VE", value: "0213", provienceName: "La Vega" },
        { id: "DO.MN", value: "0228", provienceName: "Monseñor Nouel" },
        { id: "DO.PV", value: "0517", provienceName: "Peravia" },
        { id: "DO.JO", value: "0531", provienceName: "San José de Ocoa" },
        { id: "DO.DU", value: "0306", provienceName: "Duarte" },
        { id: "DO.HM", value: "0930", provienceName: "HATO MAYOR" },
        { id: "DO.MP", value: "0929", provienceName: "MONTE PLATA" },
        { id: "DO.MT", value: "0314", provienceName: "María Trinidad Sánchez" },
        { id: "DO.SM", value: "0320", provienceName: "Samaná" },
        { id: "DO.CR", value: "0521", provienceName: "SAN CRISTÓBAL" },
        { id: "DO.NC", value: "1001", provienceName: "DISTRITO NACIONAL" },
        { id: "DO.SE", value: "0808", provienceName: "EL SEIBO" },
        { id: "DO.AL", value: "0811", provienceName: "LA ALTAGRACIA" },
        { id: "DO.RO", value: "0812", provienceName: "LA ROMANA" }
      ],
      customInnerData: [
        {
          id: "50201000000000",
          value: "10",
          municipioName: "Azua",
          provincia: "DO.AZ"
        },
        {
          id: "50202000000000",
          value: "5",
          municipioName: "Las Charcas",
          provincia: "DO.AZ"
        },
        {
          id: "50203000000000",
          value: "20",
          municipioName: "Las Yayas de Viajama",
          provincia: "DO.AZ"
        },
        {
          id: "50204000000000",
          value: "0",
          municipioName: "Padre Las Casas",
          provincia: "DO.AZ"
        },
        {
          id: "50205000000000",
          value: "0",
          municipioName: "Peralta",
          provincia: "DO.AZ"
        },
        {
          id: "50206000000000",
          value: "0",
          municipioName: "Sabana Yegua",
          provincia: "DO.AZ"
        },
        {
          id: "50207000000000",
          value: "0",
          municipioName: "Pueblo Viejo",
          provincia: "DO.AZ"
        },
        {
          id: "50208000000000",
          value: "0",
          municipioName: "Tábara Arriba",
          provincia: "DO.AZ"
        },
        {
          id: "50209000000000",
          value: "0",
          municipioName: "Guayabal",
          provincia: "DO.AZ"
        },
        {
          id: "50210000000000",
          value: "0",
          municipioName: "Estebanía",
          provincia: "DO.AZ"
        }
      ]
    };
  },

  created() {
    //  this.customData = require("@/assets/data/js/map-chart-data-test.json");
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
