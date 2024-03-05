<template>
  <div>
    <!-- select with search -->
    <select>
      <option value="erbil">Erbil</option>
      <option value="baghdad">Baghdad</option>
    </select>
    <button @click="getCoordinatesByCityName">fetch</button>
    <!-- div for result when there is : none -->
  </div>
</template>

<script>
export default {
  methods: {
    getCoordinatesByCityName() {
      const apiKey = "b58426fca9c2101b6740a4d677d35f18";
      const apiUrl = `https://api.openweathermap.org/geo/1.0/direct?q=London&appid=${apiKey}`;

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
