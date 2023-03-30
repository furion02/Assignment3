<template>
  <div>
    <h1>Current Date and Time: {{ currentDateTime }}</h1>
    <h2>Current Temperature in Paris, Ontario: {{ currentTemp }}°C</h2>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import axios from 'axios'
import { format } from 'date-fns'

export default {
  name: 'HomePage',
  setup() {
    const currentDateTime = ref('')
    const currentTemp = ref('')

    const fetchWeatherData = async () => {
      try {
        const response = await axios.get(
          'https://api.openweathermap.org/data/2.5/weather?q=Paris,ON,CA&units=metric&appid=63629b5800e7396da95e57d15251ef28'
        )
        currentTemp.value = response.data.main.temp.toFixed(1)
      } catch (error) {
        console.error(error)
      }
    }

    onMounted(() => {
      currentDateTime.value = format(new Date(), 'yyyy-MM-dd HH:mm:ss')
      fetchWeatherData()
    })

    return {
      currentDateTime,
      currentTemp,
    }
  },
}
</script>
