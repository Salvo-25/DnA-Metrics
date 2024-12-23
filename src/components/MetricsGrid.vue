<template>
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4 md:gap-6">
    <MetricCard
      v-for="metric in metrics"
      :key="metric.name"
      :label="metric.label"
      :total="metric.total"
      @click="$emit('metric-selected', metric.name)"
    />
  </div>
</template>

<script>
import MetricCard from './MetricCard.vue'

export default {
  name: 'MetricsGrid',
  components: {
    MetricCard
  },
  props: {
    metrics: {
      type: Array,
      required: true
    }
  }
}
</script>
