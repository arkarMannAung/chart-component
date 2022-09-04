<script setup lang="ts">
  import * as am5 from "@amcharts/amcharts5";
  import * as am5xy from "@amcharts/amcharts5/xy";
  import am5themes_Animated from "@amcharts/amcharts5/themes/Animated";
  import {
  onMounted, PropType
} from "vue";
import { TimeUnit } from "@amcharts/amcharts5/.internal/core/util/Time";

interface Data {
  date?: number;
  category?: string;
  value: number;
}
interface Prop {
  datas: Array<Data>;
  uniqueId: string;
  timeUnit?: string;
  width?: string;
  height?: string;
}
const props = defineProps<Prop>();
// or
// const props = defineProps({
//   data: {
//     type: Array,
//     required: true
//   }
// })

onMounted( ()=>{
  const root = am5.Root.new(props.uniqueId);
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

  const xAxis = props.datas[0].hasOwnProperty('date')?
  chart.xAxes.push(
    am5xy.DateAxis.new(root, {
    maxDeviation: 0,
    baseInterval: {
        timeUnit: props.timeUnit as TimeUnit || 'day',
        count: 1
    },
    renderer: am5xy.AxisRendererX.new(root, {}),
    tooltip: am5.Tooltip.new(root, {})
  }))
  : chart.xAxes.push(
    am5xy.CategoryAxis.new(root, {
      categoryField: "category",
      renderer: am5xy.AxisRendererX.new(root, {})
    })
  );
  if ( props.datas[0].hasOwnProperty('category') ) {
    xAxis.data.setAll( props.datas.map(data=>{
      return { category: data.category }
    }));
  }

  const yAxis = chart.yAxes.push(am5xy.ValueAxis.new(root, {
    renderer: am5xy.AxisRendererY.new(root, {})
  }));

  // date series
  const series = chart.series.push(
    am5xy.ColumnSeries.new(root, {
      name: "Series",
      xAxis: xAxis,
      yAxis: yAxis,
      valueYField: "value",
      valueXField: props.datas[0].hasOwnProperty('date')? 'date':'category',
      categoryXField: "category",
      tooltip: am5.Tooltip.new(root, {
          labelText: "{valueY}"
      })
    }
  ));

  chart.set("scrollbarX", am5.Scrollbar.new(root, {
    orientation: "horizontal"
  }));
  series.data.setAll(props.datas);
 
  series.appear(1000);
  chart.appear(1000, 100);
  });
</script>

<template>
  <div :style="{ width: props.width??'100%', height: props.height??'500px' }" :id="uniqueId" ref="columnchart"></div>
</template>

<!-- docs -->
<!-- 

Data Example

Category Data Simple
const category = [
  { category: 'dart', value: 50 },
  { category: 'php', value: 33 },
  { category: 'javascript', value: 50 },
  { category: 'python', value: 34 },
];


Date Data Simple

const today = new Date();
const next = new Date();
const date = [
  { date: next.setDate(today.getDate() + 1), value: 26 },
  { date: next.setDate(today.getDate() + 2), value: 60 },
  { date: next.setDate(today.getDate() + 3), value: 57 },
  { date: next.setDate(today.getDate() + 4), value: 45 },
  { date: next.setDate(today.getDate() + 5), value: 90 },
  { date: next.setDate(today.getDate() + 6), value: 60 },
  { date: next.setDate(today.getDate() + 7), value: 20 }
];
</script>


Category
<ColumnChartRevise 
  :datas="category" 
  uniqueId="category"
  width="100%"
  height="30px"
/>

Date
<ColumnChartRevise 
  :datas="date" 
  uniqueId="date" 
  timeUnit="day"
  width="100%"
  height="300px"
/> 
-->
