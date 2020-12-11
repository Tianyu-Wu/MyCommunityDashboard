<template>
  <div class="h-full w-full"></div>
</template>

<script>
import { loadModules } from 'esri-loader';

export default {
  name: 'web-map',
  mounted() {
    // lazy load the required ArcGIS API for JavaScript modules and CSS
    loadModules(['esri/Map', 'esri/views/MapView', 'esri/layers/FeatureLayer', "esri/widgets/Legend", "esri/widgets/LayerList","esri/widgets/Locate"], { css: true }).then(
      ([ArcGISMap, MapView, FeatureLayer, Legend,LayerList, Locate]) => {
        const map = new ArcGISMap({
          basemap: 'gray-vector',
        });

        this.view = new MapView({
          container: this.$el,
          map: map,
          center: [8.540229,47.420930],
          zoom: 13,
          ui: {components: ['zoom','compass']}
        });

        var districtLayer = new FeatureLayer({
        url: "https://services5.arcgis.com/DCFAE8AYLdyIvc7z/arcgis/rest/services/seebach/FeatureServer/0",
        title: "District Seebach",
        //*** ADD ***//
        "renderer": {
        "type": "simple",
        "symbol": {
          "type": "simple-fill",
          color: {r:0, g:185, b:216, a:0.1}
        }
      },
      "transparency": 0,
      "labelingInfo": null
      });

        // temperature layer
      var tempLayer = new FeatureLayer({
        url: "https://services5.arcgis.com/DCFAE8AYLdyIvc7z/arcgis/rest/services/self_measured_sensebox/FeatureServer/0",
        title: "Temperature",
        //*** ADD ***//
        renderer: {
          type: "simple",
          symbol: {
            type: "simple-marker",
            size: "9",
            outline: {
              width: "0.35",
              color: "white"
            }
          },
          visualVariables: [{
            type: "color",
            field: "temperature",
            layerInfos: [
              {
                title: "Temperature"
              }
            ],
            // color style with different temperature levels
            stops: [{ value: 0, color: "#93C5FD"},
            {value:5, color: "#A7F3D0"},
                  {value: 10, color: "#FDE68A"}]
          }
          ]
        },

        //*** ADD ***//
        outFields: ["ObjectId", "lat", "lon","temperature"],

        //*** ADD ***//
        popupTemplate: {  // Enable a popup
          title: "Point Id: {ObjectId}", // Show attribute value
          content: "<p>temperature: {temperature} Celsius<p>lat: {lat}</p><p>lon: {lon}</p><p>Data were collected on December 06, 2020.</p>"  // Display text in pop-up
        }
      });
      // temperature layer
      var pm10Layer = new FeatureLayer({
        url: "https://services5.arcgis.com/DCFAE8AYLdyIvc7z/arcgis/rest/services/self_measured_sensebox/FeatureServer/0",
        title: "PM 10",
        //*** ADD ***//
        renderer: {
          type: "simple",
          symbol: {
            type: "simple-marker",
            size: "9",
            outline: {
              width: "0.35",
              color: "white"
            }
          },
          visualVariables: [
          {
            type: "color",
            field: "pm10",
            layerInfos: [
              {
                title: "PM 10"
              }
            ],
            // color style with different temperature levels
            stops: [{ value: 0, color: "#C4B5FD"},
            {value:180, color: "#F9A8D4"}]
          }
          ]
        },

        //*** ADD ***//
        outFields: ["ObjectId", "lat", "lon","pm10"],

        //*** ADD ***//
        popupTemplate: {  // Enable a popup
          title: "Point Id: {ObjectId}", // Show attribute value
          content: "<p>PM 10: {pm10}µg/m3</p><p>lat: {lat}</p><p>lon: {lon}</p><p>Data were collected on December 06, 2020.</p>"  // Display text in pop-up
        }
      });
      // temperature layer
      var pm25Layer = new FeatureLayer({
        url: "https://services5.arcgis.com/DCFAE8AYLdyIvc7z/arcgis/rest/services/self_measured_sensebox/FeatureServer/0",
        title: "PM 2.5",
        //*** ADD ***//
        renderer: {
          type: "simple",
          symbol: {
            type: "simple-marker",
            size: "9",
            outline: {
              width: "0.35",
              color: "white"
            }
          },
          visualVariables: [
          {
            type: "color",
            field: "pm25",
            layerInfos: [
              {
                title: "PM 2.5"
              }
            ],
            // color style with different temperature levels
            stops: [{ value: 0, color: "#6EE7B7"},
            {value:30, color: "#FCA5A5"}]
          }
          ]
        },

        //*** ADD ***//
        outFields: ["ObjectId", "lat", "lon","pm25"],

        //*** ADD ***//
        popupTemplate: {  // Enable a popup
          title: "Point Id: {ObjectId}", // Show attribute value
          content: "<p>PM 2.5: {pm25}µg/m3</p><p>lat: {lat}</p><p>lon: {lon}</p><p>Data were collected on December 06, 2020.</p>"  // Display text in pop-up
        }
      });

      

      
      map.add(districtLayer,0)
      map.add(tempLayer, 1);
      map.add(pm10Layer, 2);
      map.add(pm25Layer, 3);

      // Add widget to the bottom right corner of the view
      var legend = new Legend({
            view: this.view,
            layout: "side-by-side"
          });
      this.view.ui.add(legend, "bottom-right");

      var layerList = new LayerList({
        view: this. view
      });
      // Adds widget below other elements in the top left corner of the view
      this.view.ui.add(layerList, {
        position: "bottom-left"
      });

      var locateBtn = new Locate({
          view: this.view
        });
        // Add the locate widget to the top left corner of the view
        this.view.ui.add(locateBtn, {
          position: "top-left"
        });


      }
    );
  },
  beforeDestroy() {
    if (this.view) {
      // destroy the map view
      this.view.destroy();
    }
  },
};
</script>
