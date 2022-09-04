<template>
  <BaseCard>
    <div class="hello" id="chartdiv" ref="columnchart"></div>
  </BaseCard>
</template>

<script setup lang="ts">
  import * as am5 from "@amcharts/amcharts5";
  import * as am5xy from "@amcharts/amcharts5/xy";
  import am5themes_Animated from "@amcharts/amcharts5/themes/Animated";
  import {
  onMounted, PropType,
} from "vue";


 interface ChartData {
  id: number;
  name: string;
  age: number;

}
const props = defineProps({
  chartSeries: Object as PropType<am5xy.ColumnSeries>,
  height: {
    type: Number
  }
})

onMounted( ()=>{
  const root = am5.Root.new("chartdiv");
  root.setThemes([am5themes_Animated.new(root)]);
  const chart = root.container.children.push(am5xy.XYChart.new(root, {
      panX: false,
      panY: false,
      wheelX: "panX",
      wheelY: "zoomX"
    }
  ));
  const cursor = chart.set("cursor", am5xy.XYCursor.new(root, {
    behavior: "zoomX"
  }));
  cursor.lineY.set("visible", false);

  let date = new Date();
  date.setHours(0, 0, 0, 0);
  let value = 100;

  function generateData() {
    value = Math.round((Math.random() * 10 - 5) + value);
    am5.time.add(date, "day", 1);
    return {
        date: date.getTime(),
        value: value
    };
  }

  function generateDatas(count: number) {
    const data = [];
    for (let i = 0; i < count; ++i) {
        data.push(generateData());
    }
    return data;
  }

  const xAxis = chart.xAxes.push(am5xy.DateAxis.new(root, {
    maxDeviation: 0,
    baseInterval: {
        timeUnit: "day",
        count: 1
    },
    renderer: am5xy.AxisRendererX.new(root, {}),
    tooltip: am5.Tooltip.new(root, {})
  }));

  const yAxis = chart.yAxes.push(am5xy.ValueAxis.new(root, {
    renderer: am5xy.AxisRendererY.new(root, {})
  }));

  const series = chart.series.push(am5xy.ColumnSeries.new(root, {
    name: "Series",
    xAxis: xAxis,
    yAxis: yAxis,
    valueYField: "value",
    valueXField: "date",
    tooltip: am5.Tooltip.new(root, {
        labelText: "{valueY}"
    })
  }));


  chart.set("scrollbarX", am5.Scrollbar.new(root, {
    orientation: "horizontal"
    }));

    let data = generateDatas(50);
    series.data.setAll(data);

    series.appear(1000);
    chart.appear(1000, 100);
  });
</script>

<style scoped>
.hello {
  width: 100%;
  height: 500px;
}
</style>
