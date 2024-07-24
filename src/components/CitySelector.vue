<template>
    <div :class="$style.container">
      <form @submit.prevent="handleSubmit" style="display: flex; align-items: center;">
        <div :class="$style.formGroup">
          <label :class="$style.formLabel">State</label>
          <select :class="$style.formControl" v-model="selectedState">
            <option value="">Select State</option>
            <option v-for="state in states" :key="state" :value="state">
              {{ state }}
            </option>
          </select>
        </div>
  
        <div :class="$style.formGroup">
          <label :class="$style.formLabel">City</label>
          <select :class="$style.formControl" v-model="selectedCity" :disabled="!selectedState">
            <option value="">Select City</option>
            <option v-for="city in cities" :key="city.City" :value="city.City">
              {{ city.City }}
            </option>
          </select>
        </div>
  
        <div :class="$style.buttonGroup">
          <button :class="$style.button" type="submit" :disabled="!selectedCity">
            <IconSearch /> Search
          </button>
          <button :class="$style.button" style="margin-left: 10px;" @click="onSearchNearby" type="button" :disabled="1" title="Currently Unavailable">
            <IconMapPin /> Nearby Search
          </button>
        </div>
      </form>
    </div>
  </template>
  
  <script>
  import { ref, onMounted, watch } from 'vue';
  import Papa from 'papaparse';
  import { IconSearch, IconMapPin } from '@tabler/icons-vue';
  
  export default {
    name: 'CitySelector',
    props: {
      onCitySelected: {
        type: Function,
        required: true
      },
      onSearchNearby: {
        type: Function,
        required: true
      }
    },
    setup(props) {
      const states = ref([]);
      const selectedState = ref('');
      const cities = ref([]);
      const selectedCity = ref('');
  
      onMounted(() => {
        Papa.parse('/output.csv', {
          download: true,
          header: true,
          complete: (results) => {
            const statesData = [...new Set(results.data.map(item => item.State))];
            states.value = statesData;
          }
        });
      });
  
      watch(selectedState, (newState) => {
        if (newState) {
          Papa.parse('/output.csv', {
            download: true,
            header: true,
            complete: (results) => {
              const cityData = results.data.filter(item => item.State === newState);
              cities.value = cityData;
              selectedCity.value = '';
            }
          });
        }
      });
  
      const handleSubmit = () => {
        const cityData = cities.value.find(city => city.City === selectedCity.value);
        if (cityData) {
          props.onCitySelected({
            state: selectedState.value,
            city: cityData.City,
            lat: parseFloat(cityData.Lat),
            lng: parseFloat(cityData.Lng),
            airbnbFile: cityData.filename
          });
          console.log(cityData.filename);
        }
      };
  
      return {
        states,
        selectedState,
        cities,
        selectedCity,
        handleSubmit
      };
    }
  };
  </script>
  
  <style module>
  .container {
  display: flex;
  align-items: center;
}

.formGroup {
  display: flex;
  align-items: center;
  margin-right: 10px;
}

.formLabel {
  margin-right: 5px;
  font-weight: bold;
}

.formControl {
  width: 150px;
  padding: 8px;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  background-color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.buttonGroup {
  display: flex;
  align-items: center;
}

.button {
  display: flex;
  align-items: center;
  padding: 8px 16px;
  background-color: #4ecdc4;
  color: #ffffff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: #45b5a8;
}

.button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}

.buttonSpace {
  margin-left: 10px;
}
  </style>
  