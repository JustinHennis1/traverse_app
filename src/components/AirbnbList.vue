<template>
    <div :class="['airbnb-list', { expanded: isExpanded }]">
      <button v-if="isExpanded" class="close-button" @click="toggleExpansion">
        Close
      </button>
      <h2 class="airbnb-title">Airbnb Listings</h2>
      <div class="scrollable-content">
        <div class="airbnb-cards">
          <div
            v-for="listing in listings"
            :key="listing.id"
            :class="['airbnb-card', { selected: selectedListing?.id === listing.id }]"
            @click="handleListingClick(listing)"
          >
            <div class="card-content">
              <img
                :src="listing.imageUrl"
                :alt="listing.name"
                class="card-image"
              />
              <div class="card-info">
                <h3 class="card-name">{{ listing.name }}</h3>
              </div>
            </div>
            <div v-if="selectedListing?.id === listing.id" class="expanded-details">
              <p class="card-description">{{ listing.description }}</p>
              <a :href="listing.url" target="_blank" rel="noopener noreferrer">
                View on Airbnb
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, watchEffect, onMounted, onUnmounted } from 'vue';
  import Papa from 'papaparse';
  
  export default {
    name: 'AirbnbList',
    props: {
      cityFileName: String,
      isExpanded: Boolean,
    },
    emits: ['toggle-expansion'],
    setup(props, { emit }) {
      const listings = ref([]);
      const selectedListing = ref(null);
  
      const loadListings = () => {
        if (props.cityFileName) {
          const filePath = `/${props.cityFileName}`;
          Papa.parse(filePath, {
            download: true,
            header: true,
            complete: function (results) {
              const filteredAndLimitedData = results.data
                .filter((listing) => parseFloat(listing.review_scores_rating) > 3.9)
                .sort((a, b) => b.review_scores_rating - a.review_scores_rating)
                .slice(0, 30);
              const mappedResults = filteredAndLimitedData.map((listing) => ({
                id: listing.id,
                name: listing.name || "No name provided",
                description:
                  listing.neighborhood_overview || "No description available.",
                imageUrl: listing.picture_url || "default-image-url",
                url: listing.listing_url,
              }));
              listings.value = mappedResults;
            },
            error: function (err) {
              console.error("Error loading Airbnb data:", err);
              listings.value = [];
            },
          });
        } else {
          listings.value = [];
        }
      };
  
      const handleListingClick = (listing) => {
        selectedListing.value = listing.id === selectedListing.value?.id ? null : listing;
      };
  
      const toggleExpansion = () => {
        emit('toggle-expansion');
      };
  
      watchEffect(() => {
        loadListings();
      });
  
      onMounted(() => {
        const handleKeyDown = (event) => {
          if (event.key === "Escape" && props.isExpanded) {
            toggleExpansion();
          }
        };
  
        window.addEventListener("keydown", handleKeyDown);
  
        onUnmounted(() => {
          window.removeEventListener("keydown", handleKeyDown);
        });
      });
  
      return {
        listings,
        selectedListing,
        handleListingClick,
        toggleExpansion,
      };
    },
  };
  </script>
  
  <style scoped>
.airbnb-list {
  margin-top: 10px;
  height: 35vh;
  display: flex;
  overflow-y: auto; /* Change from hidden to auto to enable scrolling */
  flex-direction: column;
}
  
  .airbnb-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
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
  
  .airbnb-cards {
    padding-right: 10px;
  }
  
  .airbnb-card {
    background-color: #ffffff;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    cursor: pointer;
    transition: transform 0.3s ease;
  }
  
  .airbnb-card:hover {
    transform: translateY(-5px);
  }
  
  .selected {
    background-color: #f0f0f0;
  }
  
  .card-content {
    display: flex;
    align-items: center;
  }
  
  .card-image {
    width: 100px;
    height: 100px;
    border-radius: 8px;
    margin-right: 20px;
  }
  
  .card-info {
    flex-grow: 1;
  }
  
  .card-name {
    font-size: 20px;
    color: #333333;
    margin-bottom: 5px;
  }
  
  .card-description {
    font-size: 16px;
    color: #555555;
    margin-bottom: 10px;
  }
  
  .expanded-details {
    margin-top: 20px;
  }
  
  .expanded-details a {
    color: #007bff;
    text-decoration: none;
  }
  
  .expanded {
    position: relative;
    top: 0;
    left: 0;
    width: 100vh;
    height: 60vh;
    z-index: 1;
    background-color: white;
  }
  
  .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    /* Add additional styles for the close button */
  }
  </style>