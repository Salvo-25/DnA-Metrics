<template>
  <div 
    @click="$emit('click')"
    class="p-4 md:p-6 bg-white rounded-lg shadow hover:shadow-md transition-shadow duration-300 cursor-pointer"
  >
    <h3 class="text-base md:text-lg font-medium text-gray-700">{{ label }}</h3>
    <p class="mt-2 text-2xl md:text-3xl font-semibold text-indigo-600">{{ total }}</p>
  </div>
</template>

<script>
export default {
  name: 'MetricCard',
  props: {
    label: {
      type: String,
      required: true
    },
    total: {
      type: [Number, String],
      required: true
    }
  }
}
</script>
