<template>
  <div>
    <!-- Aggiunta Header -->
    <Header />
    
    <!-- Dashboard -->
    <div class="p-4 md:p-6 space-y-6">
      <TimeSeriesChart
        v-if="currentChartData"
        :chart-data="currentChartData"
        :title="chartTitle"
        class="mb-6"
      />
      
      <MetricsGrid
        :metrics="metrics"
        @metric-selected="updateSelectedMetric"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from "../components/Header.vue";
import TimeSeriesChart from "../components/TimeSeriesChart.vue";
import MetricsGrid from "../components/MetricsGrid.vue";

export default {
  name: "TrafficDashboard",
  components: {
    Header,
    TimeSeriesChart,
    MetricsGrid,
  },
  data() {
    return {
      metrics: [
        { name: "subscriptions", label: "Subscriptions", total: 0, data: [] },
        { name: "impressions", label: "Impressions", total: 0, data: [] },
        { name: "clicks", label: "Clicks", total: 0, data: [] },
        { name: "avgTime", label: "Average Time (s)", total: 0, data: [] },
      ],
      selectedMetric: "subscriptions",
      currentChartData: null,
    };
  },
  computed: {
    chartTitle() {
      const metric = this.metrics.find((m) => m.name === this.selectedMetric);
      return metric ? `${metric.label} Trend` : "";
    },
  },
  async created() {
    await this.fetchData();
    this.updateSelectedMetric("subscriptions");
  },
  methods: {
    async fetchData() {
      const response = await axios.get(
        "https://ott-fogliata.github.io/vuejs-s2i-repository/stats.json"
      );
      const data = response.data;

      this.metrics = this.metrics.map((metric) => ({
        ...metric,
        total: data[metric.name].total,
        data: Object.entries(data[metric.name].history).map(
          ([date, value]) => ({
            date,
            value,
          })
        ),
      }));
    },
    updateSelectedMetric(metricName) {
      this.selectedMetric = metricName;
      const selectedMetric = this.metrics.find((m) => m.name === metricName);

      this.currentChartData = {
        labels: selectedMetric.data.map((item) => item.date),
        datasets: [
          {
            label: selectedMetric.label,
            backgroundColor: "rgba(99, 102, 241, 0.2)",
            borderColor: "rgb(99, 102, 241)",
            data: selectedMetric.data.map((item) => item.value),
            fill: true,
          },
        ],
      };
    },
  },
};
</script>
