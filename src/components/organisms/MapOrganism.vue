<template>
  <div id="map" class="h-screen"></div>
</template>

<script setup>
import leaflet from "leaflet";
import { onMounted } from "vue";
import { useGeolocation } from "@vueuse/core"
import { Autolinker } from "autolinker"

// import { userMarker, nearbyMarker } from "@/maps/maps";

const { coords } = useGeolocation()

onMounted(() => {
  var map = leaflet
    .map("map", {
      zoomControl:false, maxZoom:28, minZoom:1
    })
    .fitBounds([[-8.055466807586871,105.2544427411724],[-5.572093879886214,110.3864025959218]]);

  // leaflet.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
  //     maxZoom: 19,
  //     attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
  // }).addTo(map);
  // map.attributionControl.setPrefix('<a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');

  var autolinker = new Autolinker({truncate: {length: 30, location: 'smart'}});

  // remove popup's row if "visible-with-data"
  function removeEmptyRowsFromPopupContent(content, feature) {
    var tempDiv = document.createElement('div');
    tempDiv.innerHTML = content;
    var rows = tempDiv.querySelectorAll('tr');
    for (var i = 0; i < rows.length; i++) {
      var td = rows[i].querySelector('td.visible-with-data');
      var key = td ? td.id : '';
      if (td && td.classList.contains('visible-with-data') && feature.properties[key] == null) {
        rows[i].parentNode.removeChild(rows[i]);
      }
    }
    return tempDiv.innerHTML;
  }

  // add class to format popup if it contains media
  function addClassToPopupIfMedia(content, popup) {
    var tempDiv = document.createElement('div');
    tempDiv.innerHTML = content;
    if (tempDiv.querySelector('td img')) {
      popup._contentNode.classList.add('media');
      // Delay to force the redraw
      setTimeout(function() {
        popup.update();
      }, 10);
    } else {
      popup._contentNode.classList.remove('media');
    }
  }

  var zoomControl = leaflet.control.zoom({
      position: 'topleft'
  }).addTo(map);

  var bounds_group = new leaflet.featureGroup([]);

  function setBounds() {
  }

  map.createPane('pane_EsriGray_0');
  map.getPane('pane_EsriGray_0').style.zIndex = 400;
  var layer_EsriGray_0 = L.tileLayer(
    'http://services.arcgisonline.com/ArcGIS/rest/services/Canvas/World_Light_Gray_Base/MapServer/tile/{z}/{y}/{x}', {
    pane: 'pane_EsriGray_0',
    opacity: 1.0,
    attribution: '',
    minZoom: 1,
    maxZoom: 28,
    minNativeZoom: 0,
    maxNativeZoom: 18
  });
  map.addLayer(layer_EsriGray_0);

  function pop_geom_kabkota_pizza_1(feature, layer) {
    var popupContent = '<table>\
            <tr>\
                <th scope="row">pt_id</th>\
                <td class="visible-with-data" id="pt_id">' + (feature.properties['pt_id'] !== null ? autolinker.link(feature.properties['pt_id'].toLocaleString()) : '') + '</td>\
            </tr>\
            <tr>\
                <th scope="row">seg_id</th>\
                <td class="visible-with-data" id="seg_id">' + (feature.properties['seg_id'] !== null ? autolinker.link(feature.properties['seg_id'].toLocaleString()) : '') + '</td>\
            </tr>\
            <tr>\
                <th scope="row">ring_id</th>\
                <td class="visible-with-data" id="ring_id">' + (feature.properties['ring_id'] !== null ? autolinker.link(feature.properties['ring_id'].toLocaleString()) : '') + '</td>\
            </tr>\
        </table>';
    var content = removeEmptyRowsFromPopupContent(popupContent, feature);
    layer.on('popupopen', function(e) {
      addClassToPopupIfMedia(content, e.popup);
    });
    layer.bindPopup(content, { maxHeight: 400 });
  }
  function style_geom_kabkota_pizza_1_0() {
    return {
      pane: 'pane_geom_kabkota_pizza_1',
      opacity: 1,
      color: 'rgba(35,35,35,1.0)',
      dashArray: '',
      lineCap: 'butt',
      lineJoin: 'miter',
      weight: 1.0, 
      fill: true,
      fillOpacity: 1,
      fillColor: 'rgba(114,155,111,1.0)',
      interactive: true,
    }
  }
  map.createPane('pane_geom_kabkota_pizza_1');
  map.getPane('pane_geom_kabkota_pizza_1').style.zIndex = 401;
  map.getPane('pane_geom_kabkota_pizza_1').style['mix-blend-mode'] = 'normal';
  var layer_geom_kabkota_pizza_1 = new L.geoJson(json_geom_kabkota_pizza_1, {
      attribution: '',
      interactive: true,
      dataVar: 'json_geom_kabkota_pizza_1',
      layerName: 'layer_geom_kabkota_pizza_1',
      pane: 'pane_geom_kabkota_pizza_1',
      onEachFeature: pop_geom_kabkota_pizza_1,
      style: style_geom_kabkota_pizza_1_0,
  });
});
</script>