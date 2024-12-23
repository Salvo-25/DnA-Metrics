<template>
  <div class="min-h-screen bg-gray-50">
    <TrafficDashboard />
  </div>
</template>

<script>
import TrafficDashboard from './views/TrafficDashboard.vue'

export default {
  name: 'App',
  components: {
    TrafficDashboard
  }
}
</script>