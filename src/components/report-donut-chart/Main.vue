<template>
  <Chart
    type="doughnut"
    :width="width"
    :height="height"
    :data="data"
    :options="options"
  />
</template>

<script setup>
import { computed } from "vue";
import { useDarkModeStore } from "@/stores/dark-mode";
import { useColorSchemeStore } from "@/stores/color-scheme";
import { colors } from "@/utils/colors";

const props = defineProps({
  width: {
    type: Number,
    default: 0,
  },
  height: {
    type: Number,
    default: 0,
  },
});

const darkMode = computed(() => useDarkModeStore().darkMode);
const colorScheme = computed(() => useColorSchemeStore().colorScheme);

const chartData = [15, 10, 65];
const chartColors = () => [
  colors.pending(0.9),
  colors.warning(0.9),
  colors.primary(0.9),
];

const data = computed(() => {
  return {
    labels: ["31 - 50 Years old", ">= 50 Years old", "17 - 30 Years old"],
    datasets: [
      {
        data: chartData,
        backgroundColor: colorScheme.value ? chartColors() : "",
        hoverBackgroundColor: colorScheme.value ? chartColors() : "",
        borderWidth: 5,
        borderColor: darkMode.value ? colors.darkmode[700]() : colors.white,
      },
    ],
  };
});

const options = computed(() => {
  return {
    maintainAspectRatio: false,
    legend: {
      display: false,
    },
    cutoutPercentage: 80,
  };
});
</script>
