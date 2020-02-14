# dominican-map-component

## Installation
```
npm install dominican-map

```

### Usage
```
<template>
  <section>
    <dominican-map
      v-bind:hasToolTipMessage="true"
      v-bind:hasToolTipMessageDetailMap="true"
      mapToolTipMessage="Total de edificaciones actuales:"
      toolTipValue="value"
      detailMapToolTip="Totales:"
      detailMapToolTipValue="numberOfRequests"
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
      v-bind:isBackButtonVisible="true"
    ></dominican-map>
  </section>
</template>

<script>
import DominicanMap from "dominican-map";
import "dominican-map/dist/dominican.css";

export default {  
  name: "app",
  components: {
    DominicanMap
  },
  data() {
    return {
      
    };
  },
  created() {
  }
};
</script>


```

### Props:
```
hasToolTipMessage: is set to true by default, with this prop you can specify if you wish to provide a toolTipMessage when the user hover's over a provience.

hasToolTipMessageDetailMap: is set to true by default, with this prop you can specify if you wish to provide a toolTipMessage over the town the user has clicked.

mapToolTipMessage: you can specify the message to display to the user when they hovers a provience/town.

toolTipValue: is set to "value" by default, you can provide the property name from your object data.

detailMapToolTip:"you can specify the message to display to the user when they hovers a provience/town."

detailMapToolTipValue: is set to "value" by default, you can provide the property name from your object data.

fromMainMapValue: with this prop you can set the amount from where do you want to have an X. Default value : 0
 
toMainMapValue: with this prop you can set the amount until you want your provience/town to display X color. Default value : 200

greaterThanMainMapValue: with this prop you can set a different color, starting at a X value: Default value: 201.

fromToDetailedMapColor: with this prop you can set the amount from where do you want to have an X color for the 
country map. Default value: 0
 
greaterThanDetailedMapValue: with this prop you can set the amount until you want your provience/town to display X color
for the country map . Default value: 200

greaterThanDetailedMapColor: with this prop you can set a different color, starting at a X value
for the country map: Default value: 201.

isBackButtonVisible: property to show the back buttom once we already drill in the map.

buttonMessage: display text on the button to ''go back'' when drilling in the town.

mapDataSrc: custom JSON you can provide for the main map data.

innerMapCustomData: custom JSON you provide for the town data, using the object property "provincia" to replace the default data with yours.

```

### Working with custom data for the main map: 
```
In order for you to work with custom data, you need to define in your API an object property to link with the specified city the user will hover (id) for example.
	
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

the "value", is the info you would like to display on hover, the provienceName we don't really need to specify that, do we :) ? 

```

### Working with custom data for towns: 
```
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
In a real case the array will include the entire object info for all towns, the "value", is the info you would like to display on hover the municipioName is the name of each town in the provience,
and the provincia is the key that your entire provience object should have for each specific town. You can see the full provience keys (id and provincia) [here](https://github.com/taverasady/dominican-map/tree/master/src/assets/data/json/provincias).

```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
