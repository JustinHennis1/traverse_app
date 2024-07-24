<template>
  <div class="app-container">
    <Header @citySelected="handleCitySelected" @searchNearby="fetchNearbyData" />
    <LoadingSpinner v-if="isLoading" />
    <Body
      v-else
      :location="location"
      :airbnbFile="airbnbFile"
      :cityName="cityName"
      :nearbyLocations="nearbyLocations"
    />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import "bootstrap/dist/css/bootstrap.min.css";
import Header from './components/Header.vue';
import Body from './components/Body.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

export default {
  name: 'App',
  components: {
    Header,
    Body,
    LoadingSpinner
  },
  setup() {
    const location = ref({ lat: 39.905714, lng: 116.391297 });
    const airbnbFile = ref('');
    const cityName = ref('');
    const nearbyLocations = ref(null);
    const isLoading = ref(false);

    onMounted(() => {
      fetchUserLocation();
    });

    const fetchUserLocation = () => {
      return new Promise((resolve, reject) => {
        navigator.geolocation.getCurrentPosition(
          (position) => {
            const { latitude, longitude } = position.coords;
            location.value = { lat: latitude, lng: longitude };
            console.log("User location fetched:", { latitude, longitude });
            resolve({ latitude, longitude });
          },
          (error) => {
            console.error("Error fetching user location:", error);
            reject(error);
          }
        );
      });
    };

    const fetchNearbyData = async () => {
      isLoading.value = true;

      try {
        const { latitude, longitude } = await fetchUserLocation();
        const nearbyResponse = await fetch('http://127.0.0.1:5000/nearbySearch', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({ Latitude: latitude, Longitude: longitude })
        });

        if (!nearbyResponse.ok) {
          throw new Error('Network response was not ok');
        }

        await handleSearchNearby();
      } catch (error) {
        console.error('There was a problem with the fetch operation:', error);
      } finally {
        isLoading.value = false;
      }
    };

    const handleCitySelected = (cityInfo) => {
      location.value = { lat: cityInfo.lat, lng: cityInfo.lng };
      airbnbFile.value = cityInfo.airbnbFile;
      cityName.value = cityInfo.city;
    };

    const handleSearchNearby = async () => {
      cityName.value = '';
      airbnbFile.value = '';
      const response = await fetch('http://127.0.0.1:5000/nearby.csv', { method: 'GET' });
      const csvData = await response.text();
      console.log("CSV data fetched:", csvData);
      if (csvData) {
        nearbyLocations.value = true;
      }
    };

    return {
      location,
      airbnbFile,
      cityName,
      nearbyLocations,
      isLoading,
      fetchNearbyData,
      handleCitySelected,
    };
  }
};
</script>

<style scoped>
.app-container {
 
  display: flex;
  flex-direction: column;
  width: 100vw;
  height: 100vh;
  background-color: #f5f5f5;
  font-family: "Roboto", sans-serif;
}
</style>