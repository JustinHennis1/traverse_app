<template>
    <div ref="mapContainer" class="map-container"></div>
  </template>
  
  <script>
  import { ref, onMounted, watch, onUnmounted } from 'vue';
  import L from 'leaflet';
  import 'leaflet/dist/leaflet.css';
  
  export default {
    name: 'MapDisplay',
    props: {
      location: {
        type: Object,
        required: true,
      },
      userLocation: {
        type: Object,
        default: null,
      },
      selectedItinerary: {
        type: Object,
        default: null,
      },
    },
    setup(props) {
      const mapContainer = ref(null);
      let map = null;
      let marker = null;
  
      const initMap = () => {
        if (mapContainer.value && !map) {
          map = L.map(mapContainer.value, {
            center: [props.location.lat, props.location.lng],
            zoom: 13,
          });
  
          L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution:
              '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
          }).addTo(map);
        }
      };
  
      const updateMap = () => {
        if (map) {
          const mainIcon = L.icon({
            iconUrl:
              'https://cdn.rawgit.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-blue.png',
            shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png',
            iconSize: [25, 41],
            iconAnchor: [12, 41],
            popupAnchor: [1, -34],
            tooltipAnchor: [16, -28],
            shadowSize: [41, 41],
          });
  
          map.setView([props.location.lat, props.location.lng]);
          L.marker([props.location.lat, props.location.lng], { icon: mainIcon }).addTo(map);
  
          if (props.userLocation) {
            map.setView([props.userLocation.lat, props.userLocation.lng]);
            L.marker([props.userLocation.lat, props.userLocation.lng], {
              icon: mainIcon,
            }).addTo(map);
          }
        }
      };
  
      const updateSelectedItinerary = () => {
        if (map && props.selectedItinerary) {
          if (marker) {
            map.removeLayer(marker);
          }
  
          const itineraryIcon = L.icon({
            iconUrl:
              'https://cdn.rawgit.com/pointhi/leaflet-color-markers/master/img/marker-icon-2x-red.png',
            shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/0.7.7/images/marker-shadow.png',
            iconSize: [25, 41],
            iconAnchor: [12, 41],
            popupAnchor: [1, -34],
            tooltipAnchor: [16, -28],
            shadowSize: [41, 41],
          });
  
          marker = L.marker(
            [props.selectedItinerary.latitude, props.selectedItinerary.longitude],
            { icon: itineraryIcon }
          ).addTo(map);
  
          map.setView(
            [props.selectedItinerary.latitude, props.selectedItinerary.longitude],
            13
          );
        } else if (map && marker) {
          map.removeLayer(marker);
          marker = null;
          map.setView([props.location.lat, props.location.lng], 13);
        }
      };
  
      onMounted(() => {
        initMap();
        updateMap();
      });
  
      watch(() => props.location, updateMap);
      watch(() => props.userLocation, updateMap);
      watch(() => props.selectedItinerary, updateSelectedItinerary);
  
      onUnmounted(() => {
        if (map) {
          map.remove();
          map = null;
        }
      });
  
      return {
        mapContainer,
      };
    },
  };
  </script>
  
  <style scoped>
  .map-container {
    width: auto;
    height: 100%;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .itinerary-icon {
    filter: hue-rotate(120deg);
  }
  </style>