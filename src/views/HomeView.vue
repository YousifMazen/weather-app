<template>
  <div>
    <!-- select with search -->
    <select v-model="selectedCity">
      <option value="erbil">Erbil</option>
      <option value="baghdad">Baghdad</option>
    </select>
    <button @click="getCoordinatesByCityName">fetch</button>
    <!-- div for result when there is : none -->
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedCity: "erbil",
      wweatherData: null,
    };
  },
  methods: {
    getCoordinatesByCityName() {
      const apiKey = "";
      const apiUrl = `https://api.openweathermap.org/geo/1.0/direct?q=${this.selectedCity}&appid=${apiKey}`;

      fetch(apiUrl)
        .then((response) => {
          if (!response.ok) {
            throw new Error("Network response was not ok");
          }
          return response.json();
        })
        .then((data) => {
          console.log(data);
          if (data.length > 0) {
            let lat = data[0].lat;
            let lon = data[0].lon;
            this.getWeatherByCoordinates(lat, lon);
          } else {
            console.error("No data found for the selected city");
          }
        })
        .catch((error) => {
          console.error("There was a problem with the fetch operation:", error);
        });
    },

    getWeatherByCoordinates(lat, lon) {
      const apiKey = "";
      const apiUrl = `https://api.openweathermap.org/data/3.0/onecall?lat=${lat}&lon=${lon}&appid=${apiKey}`;

      fetch(apiUrl)
        .then((response) => {
          if (!response.ok) {
            throw new Error("Network response was not ok");
          }
          return response.json();
        })
        .then((data) => {
          console.log(data);
        })
        .catch((error) => {
          console.error("There was a problem with the fetch operation:", error);
        });
    },
  },
};
</script>

<style></style>
