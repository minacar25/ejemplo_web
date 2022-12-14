<template>
  <Chart
    type="line"
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

const data = computed(() => {
  return {
    labels: [
      "Jan",
      "Feb",
      "Mar",
      "Apr",
      "May",
      "Jun",
      "Jul",
      "Aug",
      "Sep",
      "Oct",
      "Nov",
      "Dec",
    ],
    datasets: [
      {
        label: "Html Template",
        data: [0, 200, 250, 200, 500, 450, 850, 1050, 950, 1100, 900, 1200],
        borderWidth: 2,
        borderColor: colorScheme.value ? colors.primary() : "",
        backgroundColor: "transparent",
        pointBorderColor: "transparent",
      },
      {
        label: "VueJs Template",
        data: [0, 300, 400, 560, 320, 600, 720, 850, 690, 805, 1200, 1010],
        borderWidth: 2,
        borderDash: [2, 2],
        borderColor: darkMode.value
          ? colors.slate["400"](0.6)
          : colors.slate["400"](),
        backgroundColor: "transparent",
        pointBorderColor: "transparent",
      },
    ],
  };
});

const options = computed(() => {
  return {
    legend: {
      labels: {
        fontColor: colors.slate["500"](0.8),
      },
    },
    scales: {
      xAxes: [
        {
          ticks: {
            fontSize: "12",
            fontColor: colors.slate["500"](0.8),
          },
          gridLines: {
            display: false,
          },
        },
      ],
      yAxes: [
        {
          ticks: {
            fontSize: "12",
            fontColor: colors.slate["500"](0.8),
            callback: function (value) {
              return "$" + value;
            },
          },
          gridLines: {
            color: darkMode.value
              ? colors.slate["500"](0.3)
              : colors.slate["300"](),
            zeroLineColor: darkMode.value
              ? colors.slate["500"](0.3)
              : colors.slate["300"](),
            borderDash: [2, 2],
            zeroLineBorderDash: [2, 2],
            drawBorder: false,
          },
        },
      ],
    },
  };
});
</script>
