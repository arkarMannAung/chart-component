<script setup lang="ts">
import { onMounted, ref } from 'vue';
// import * as am5 from '@amcharts/amcharts5';
// import * as am5xy from '@amcharts/amcharts5/xy';
// import am5themes_Animated from '@amcharts/amcharts5/themes/Animated';

// interface Props {
//     users: Array<Users>;
// }
interface Users {
    name: string;
    age: Number;
}
// const props = defineProps<Props>();
const props = defineProps({
    users: {
        type: Array,
        required: true,
    }
})
onMounted( ()=>{
    
});
</script>
<template>
    <div class="grid grid-cols-4 gap-8">
        <div v-for="user in users" :key="user.id" class="">
            <div class="rounded-lg p-8 flex-col bg-pink-300 w-[300px]">
                <div class="my-2">
                    name: {{user.name}}
                </div>
                <div class="my-2">
                    age: {{user.age}}
                </div>
            </div>
        </div>
    </div>
    
</template>