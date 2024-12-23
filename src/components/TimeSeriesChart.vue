<template>
  <div class="bg-white rounded-lg shadow p-4 md:p-6">
    <div class="h-[300px] md:h-[400px]">
      <Line
        v-if="chartData"
        :data="chartData"
        :options="chartOptions"
      />
    </div>
  </div>
</template>

<script>
import { Line } from 'vue-chartjs'
import {
  Chart as ChartJS,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend,
  Filler
} from 'chart.js'

ChartJS.register(
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
  Title,
  Tooltip,
  Legend,
  Filler
)

export default {
  name: 'TimeSeriesChart',
  components: {
    Line
  },
  props: {
    chartData: {
      type: Object,
      required: true
    },
    title: {
      type: String,
      required: true
    }
  },
  computed: {
    chartOptions() {
      return {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            position: 'top'
          },
          title: {
            display: true,
            text: this.title,
            font: {
              size: 16,
              weight: 'medium'
            }
          }
        }
      }
    }
  }
}
</script>
