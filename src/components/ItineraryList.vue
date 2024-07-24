<template>
    <div class="itineraryList">
      <div class="scrollable-content" ref="scrollContent">
        <div class="itineraryCards">
          <div
            v-for="itinerary in filteredItineraries"
            :key="itinerary.id"
            :class="['itineraryCard', { selected: selectedItinerary?.id === itinerary.id }]"
            @click="handleItineraryClick(itinerary)"
          >
            <div class="cardHeader">
              <img
                :src="itinerary.iconUrl || defaultImage"
                alt="Location Icon"
                class="iconStyle"
              />
              <div>
                <h3>{{ itinerary.title }}</h3>
                <p class="itineraryAddress">{{ itinerary.address }}</p>
                <p v-if="itinerary.rating" class="itineraryRating">
                  Rating: {{ itinerary.rating }} ({{ itinerary.totalRatings }} ratings)
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, computed, watch, onMounted } from 'vue';
  import Papa from 'papaparse';
  import defaultImage from '../logo.png';
  
  export default {
    name: 'ItineraryList',
    props: {
      cityFileName: String,
      cityName: String,
      nearbyLocations: Boolean,
    },
    emits: ['itinerary-select'],
    setup(props, { emit }) {
      const itineraries = ref([]);
      const selectedItinerary = ref(null);
      const selectedTags = ref([]);
      const uniqueTags = ref([]);
      const scrollContent = ref(null);
  
      const filteredItineraries = computed(() => {
        return selectedTags.value.length
          ? itineraries.value.filter((itinerary) =>
              selectedTags.value.every((tag) => itinerary.tags.includes(tag))
            )
          : itineraries.value;
      });
  
      const handleItineraryClick = (itinerary) => {
        selectedItinerary.value = selectedItinerary.value?.id === itinerary.id ? null : itinerary;
        emit('itinerary-select', selectedItinerary.value);
      };
  
      const getNearbyList = () => {
        const filePath = `/nearby.csv`;
        Papa.parse(filePath, {
          download: true,
          header: true,
          complete: function (results) {
            const uniqueCoordinates = new Set();
            const nearbyItineraries = [];
            results.data.forEach((itinerary) => {
              const latitude = itinerary.Latitude;
              const longitude = itinerary.Longitude;
              const coordinates = `${latitude},${longitude}`;
              const isValidItinerary =
                latitude &&
                longitude &&
                itinerary.Name &&
                itinerary.Address &&
                itinerary.City &&
                itinerary.State &&
                itinerary.Type;
  
              if (isValidItinerary && !uniqueCoordinates.has(coordinates)) {
                nearbyItineraries.push({
                  id: itinerary["Index"],
                  title: itinerary.Name,
                  address: itinerary.Address,
                  city: itinerary.City,
                  state: itinerary.State,
                  description: itinerary.Type,
                  rating: itinerary.Rating,
                  totalRatings: itinerary["Total Ratings"],
                  latitude: latitude,
                  longitude: longitude,
                  iconUrl: itinerary["Icon URL"],
                  tags: getTags(itinerary),
                });
                uniqueCoordinates.add(coordinates);
              }
            });
            itineraries.value = nearbyItineraries;
          },
          error: function (err) {
            console.error("Error loading nearby locations data:", err);
            itineraries.value = [];
          },
        });
      };
  
      const getTags = (itinerary) => {
        const types = (itinerary.Type || '').split(", ").filter(
          (type) => type !== "Point Of Interest" && type !== "Establishment"
        );
        return types.map((type) => type.trim());
      };
  
      watch(() => props.cityFileName, () => {
        if (props.cityFileName) {
          const filePath = `/all_cities_top_places.csv`;
          Papa.parse(filePath, {
            download: true,
            header: true,
            complete: function (results) {
              const filteredItineraries = results.data
                .filter((itinerary) => itinerary.City === props.cityName)
                .map((itinerary) => ({
                  id: itinerary["Place ID"],
                  title: itinerary.Name,
                  address: itinerary.Address,
                  city: itinerary.City,
                  state: itinerary.State,
                  description: itinerary.Type,
                  rating: itinerary.Rating,
                  totalRatings: itinerary["Total Ratings"],
                  latitude: itinerary.Latitude,
                  longitude: itinerary.Longitude,
                  iconUrl: itinerary["Icon URL"],
                  tags: getTags(itinerary),
                }));
              itineraries.value = filteredItineraries;
            },
            error: function (err) {
              console.error("Error loading itinerary data:", err);
              itineraries.value = [];
            },
          });
        } else if (props.nearbyLocations) {
          getNearbyList();
        } else {
          getNearbyList();
        }
      }, { immediate: true });
  
      watch(itineraries, () => {
        if (itineraries.value.length > 0) {
          uniqueTags.value = [...new Set(itineraries.value.flatMap((itinerary) => itinerary.tags))];
        }
      });
  
      watch(selectedItinerary, () => {
        if (selectedItinerary.value && scrollContent.value) {
          const selectedCard = scrollContent.value.querySelector('.itinerary-card.selected');
          if (selectedCard) {
            selectedCard.scrollIntoView({ behavior: 'smooth', block: 'center' });
          }
        }
      });
  
      return {
        itineraries,
        selectedItinerary,
        filteredItineraries,
        handleItineraryClick,
        scrollContent,
        defaultImage,
      };
    },
  };
  </script>
  
  <style scoped>

.scrollable-content {
  flex: 1;
  overflow-y: auto;
  scrollbar-width: thin; /* Thin scrollbar for Firefox */
  scrollbar-color: #000 #fff; /* Black thumb and white track for Firefox */
}

/* WebKit-based browsers (Chrome, Safari) */
.scrollable-content::-webkit-scrollbar {
  width: 12px; /* Width of the scrollbar */
}

.scrollable-content::-webkit-scrollbar-track {
  background: #fff; /* White background for the track */
  border-radius: 6px; /* Rounded corners for the track */
}

.scrollable-content::-webkit-scrollbar-thumb {
  background: #000; /* Black color for the thumb */
  border-radius: 6px; /* Rounded corners for the thumb */
  border: 3px solid #fff; /* White border around the thumb for contrast */
}

.scrollable-content::-webkit-scrollbar-thumb:hover {
  background: #333; /* Slightly lighter black for hover effect */
}

  .itineraryList {
  margin-top: 20px;
  height: 65vh;
  align-items: flex-end;
  display: flex;
  flex-direction: column;
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 10px;
}

.itineraryTitle {
  font-size: 24px;
  font-weight: bold;
}

.filterDropdown {
  position: relative;
}

.dropdownHeader {
  display: flex;
  align-items: center;
  padding: 6px 10px;
  background-color: #f0f0f0;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.dropdownHeader:hover {
  background-color: #e0e0e0;
}

.dropdownMenu {
  position: absolute;
  top: 100%;
  right: 0;
  z-index: 1;
  width: 200px;
  background-color: #ffffff;
  border-radius: 4px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.dropdownItem {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.dropdownItem:hover {
  background-color: #f0f0f0;
}

.selectedTag {
  background-color: #007bff;
  color: #ffffff;
}

.tagCount {
  font-size: 14px;
  color: #777777;
}

.itineraryCards {
  flex: 1;
  overflow: hidden;
}

.itineraryCard {
  background-color: #ffffff;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  transition: transform 0.3s ease;
  display: flex;
  flex-direction: column;
  align-items: start;
}

.itineraryCard:hover {
  transform: translateY(-5px);
}

.selected {
  background-color: #f0f0f0;
}

.itineraryAddress {
  font-size: 16px;
  color: #777777;
  margin-bottom: 5px;
}

.itineraryRating {
  font-size: 16px;
  color: #007bff;
  margin-bottom: 5px;
}

.detailsContainer {
  margin-top: 20px;
  font-size: 16px;
  color: #555555;
}

.cardHeader {
  display: flex;
  align-items: center;
}

.iconStyle {
  width: 60px;
  margin-right: 20px;
}

.dropdownItem {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.dropdownItem:hover {
  background-color: #f0f0f0;
}

.selectedTag {
  background-color: #007bff;
  color: #ffffff;
}

.selectedTag:hover {
  background-color: #0056b3;
}

.tagCount {
  font-size: 14px;
  color: #777777;
}

.checkIcon {
  margin-left: 8px;
  color: #ffffff;
}

.clearFilters {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px;
  background-color: #f0f0f0;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.clearFilters:hover {
  background-color: #e0e0e0;
}

.clearFilters span {
  margin-left: 8px;
}
  </style>