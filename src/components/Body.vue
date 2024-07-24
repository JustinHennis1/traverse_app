<template>
    <div class="body-container">
      <div class="map-and-airbnb-section">
        <div :class="['map-section', { 'map-section-close': isAirbnbExpanded }]">
          <MapDisplay :location="location" :selectedItinerary="selectedItinerary" />
        </div>
        
        <button @click="toggleAirbnbExpansion">
          {{ isAirbnbExpanded ? "Collapse Airbnb List" : "Expand Airbnb List" }}
        </button>
        
        <div :class="['airbnb-section', { 'airbnb-section-expanded': isAirbnbExpanded }]">
          <AirbnbList
            :cityFileName="airbnbFile"
            :isExpanded="isAirbnbExpanded"
            @toggle-expansion="toggleAirbnbExpansion"
          />
        </div>
      </div>
      
      <div :class="['itinerary-section', { 'itinerary-section-moved': isAirbnbExpanded }]">
        <ItineraryList
          :cityFileName="airbnbFile"
          :cityName="cityName"
          @itinerary-select="handleItinerarySelect"
          :nearbyLocations="nearbyLocations"
        />
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  import MapDisplay from './MapDisplay.vue';
  import ItineraryList from './ItineraryList.vue';
  import AirbnbList from './AirbnbList.vue';
  
  export default {
    name: 'Body',
    components: {
      MapDisplay,
      ItineraryList,
      AirbnbList
    },
    props: {
      location: {
        type: Object,
        required: true
      },
      airbnbFile: {
        type: String,
        required: true
      },
      cityName: {
        type: String,
        required: true
      },
      nearbyLocations: {
        type: Boolean,
        default: false
      }
    },
    setup() {
      const selectedItinerary = ref(null);
      const isAirbnbExpanded = ref(false);
  
      const handleItinerarySelect = (itinerary) => {
        selectedItinerary.value = itinerary;
      };
  
      const toggleAirbnbExpansion = () => {
        isAirbnbExpanded.value = !isAirbnbExpanded.value;
      };
  
      return {
        selectedItinerary,
        isAirbnbExpanded,
        handleItinerarySelect,
        toggleAirbnbExpansion
      };
    }
  };
  </script>
  
  <style scoped>
  .body-container {
    display: flex;
    flex: 1;
    padding: 20px;
  }
  
  .map-and-airbnb-section {
    flex: 0.4;
    display: flex;
    flex-direction: column;
  }
  
  .map-section {
    flex: 1;
  }
  
  .map-section-close {
    display: none;
  }
  
  .airbnb-section {
    margin-top: 20px;
    flex: 1;
    background-color: #ffffff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .airbnb-section-expanded {
    width: 100%;
    height: 20%;
  }
  
  .itinerary-section {
    flex: 0.6;
    background-color: #ffffff;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    padding: 20px;
    margin-left: 20px;
  }
  
  .itinerary-section-moved {
    border: 2px solid black;
  }
  </style>