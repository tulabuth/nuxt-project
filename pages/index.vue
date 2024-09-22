<script setup>
import { Tabs, TabsContent, TabsList, TabsTrigger } from "@/components/ui/tabs";
import TabsToday from '@/components/Tabs/Today.vue'
import { ref } from 'vue'
import TabsWeek from "@/components/Tabs/Week.vue";
import TabsMonth from '@/components/Tabs/Month.vue';
import TabsYear from '@/components/Tabs/Year.vue';

const list = ref([
  { title: "Today", component: TabsToday },
  { title: "Week", component: TabsWeek },
  { title: "Month", component: TabsMonth },
  { title: "Year", component: TabsYear },
]);
let data = ref([5.2, 5.7, 8.7, 13.9, 18.2, 21.4, 25.0, 26.0,24.0,21.0,15.0,10.0,1.0]);

let categories = ref({
    today:[
        "00:00",
        "01:00",
        "02:00",
        "03:00",
        "04:00",
        "05:00",
        "06:00",
        "07:00",
        "08:00",
        "09:00",
        "10:00",
        "11:00",
        "12:00",
        "13:00",
        "14:00",
        "15:00",
        "16:00",
        "17:00",
        "18:00",
        "19:00",
        "20:00",
        "21:00",
        "22:00",
        "23:00",
        "24:00"
    ],
   
    week:[
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
        "Sunday"
    ],
    year:[
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
        "Dec"
    ]
})

let currentCategory = ref("today")
const setCategory =(e)=>{
    const v = e.target.innerText.toLowerCase();
    currentCategory.value = v;
    
    switch(v) {
        case 'today': 
        generateRandomData(24);
            break;
        case 'week': 
        generateRandomData(7);
            break;
        case 'month': 
        generateRandomData(31);
            break;
        case 'year': 
        generateRandomData(365);
            break;
        default: 
        generateRandomData(24);
    }
    
    
}

function generateRandomData(number =7){
    let values =[]
    for(let i=0; i<number+1; i++){
        values.push(Math.floor(Math.random()* 100))
    }
    data.value = values;
    return values;
}
 function generateMonth(){
    let currentdate = new Date();
    let currentMonth = currentdate.getMonth() + 1;
    let currentYear = currentdate.getFullYear();

    function generateMonthDates(){
        let monthDates = [];
        let daysInMonth = new Date(currentYear, currentMonth,0).getDate();

        for(let i =1; i<= daysInMonth; i++){
            let dayString = ("0" +i).slice(-2);
            let monthString = ("0"+currentMonth).slice(-2);
            monthDates.push(monthString + "/"+dayString);
        }
        return monthDates;
    }
    let month  = generateMonthDates();
    categories.value = ({...categories.value, month})
    return month;
 }
onMounted(()=>{
    generateMonth();
    generateRandomData(7);
})

const options = computed(()=>(
   {
    chart: {
        type: 'line',
        animation:{
            enabled:false
        },
    },
    title: {
        text: ''
    },
    
    xAxis: {
        gridLineColor: 'transparent',
        categories: categories.value[currentCategory.value]
    },
    yAxis: {
        gridLineColor: 'transparent',
        title:{
            text:''
        }
    },
    plotOptions: {
       line:{
        marker:{
            enabled: false
        },
        dataLabels: {
            enabled: true 
        },
        enableMouseTracking: true
       }
    },
   series:[{
    name: 'line',
    lineWidth: '4px',
    color:{
        linearGradient:{y1:0, y2:0,y3:0,y4:0},
        stops:[
            [0, 'rgba(252, 127,69,1)'],
            [0.33, 'rgba(253,29, 29,1)'],
            [0.66, 'rgba(131,58,180,1)'],
            [1, 'rgba(29,217,83,1)']
        ]
    },
    data:data.value
   }]
}

))



</script>

<template>
  <div class="grid w-full gap-4">
    <header class="flex items-start justify-between">
      <div class="grow">
        <p>Hi, welcome back Guillaume !</p>
        <h1>Dashboard</h1>
      </div>
      <div class="w-[120px] h-[36px] bg-neutral-200"></div>
    </header>
    <main class="grid gap-2">
      <Tabs default-value="Today" @click="setCategory">
        <TabsList class="max-w-[400px]">
          <TabsTrigger
            v-for="(item, index) in list"
            :key="index"
            :value="item.title"
            >{{ item.title }}</TabsTrigger
          >
        </TabsList>
        <TabsContent class="w-[100%]"
          v-for="item in list"
          :key="item.title"
          :value="item.title"
        >
        <highchart v-if="data.length > 0" :options="options"/>
        </TabsContent>
      </Tabs>
      
    </main>
    <footer>
      <div class="flex items-center gap-4">
        <div
          v-for="(item, index) in 3"
          :key="index"
          class="w-full h-[260px] bg-neutral-200"
        ></div>
      </div>
    </footer>
  </div>
</template>
