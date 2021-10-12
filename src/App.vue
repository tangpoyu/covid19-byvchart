<template>
  
  <div id="app">
      <div class="title">
        <h1>COVID-19 Tracking Dashboard of Taiwan</h1>
      </div>
      <h2>1.EverydaySuffer</h2>
      <ve-line 
        :settings="chartSettings"
        :data="chartData"
        :colors="color[0]">
      </ve-line>
      <h2>2.TotalSuffer</h2>
      <ve-line 
        :settings="chartSettings"
        :extend="chartExtend[0]"
        :data="chartData1"
        :colors="color[1]">
      </ve-line>
      <h2>3.TotalDeath</h2>
      <ve-line 
        :settings="chartSettings"
        :extend="chartExtend[1]"
        :data="chartData2"
        :colors="color[2]">
      </ve-line>
      <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/v-charts/lib/style.min.css">
  </div>
  
</template>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/v-charts/lib/index.min.js"></script>
<style>
*{
  margin:0;
  padding: 0;
  list-style: none;
}
.title{
  background-color: black;
  height: 80px;
  margin-bottom: 50px;
}
h1{
  color: aliceblue;
  text-align: center;
  padding-top: 20px;
  
}
h2{
  text-align: left;
  padding-left: 2%;
  
 
}
#app{
  margin-top: 0px;
}
</style>
<script>

import axios from 'axios'
const COLOR_LIST = ['#FFD700']

export default {
  
  name: 'App',
  
  components: {
    
  },
  
  data: function () {
        return {
          chartSettings: {
            area:true
          },
          chartExtend:[
            {'yAxis.0.min': 16000}, 
            {'yAxis.0.min': 838}
          ],
          chartData: {
            columns: ['date', 'suffer'],
            rows: [
             
            ]
          },
          chartData1: {
            columns: ['date', 'suffer'],
            rows: [
             
            ]
          },
          chartData2: {
            columns: ['date', 'suffer'],
            rows: [
             
            ]
          },
          color:[ '#EF5350','#FFF176','#FFB74D']
        }
  },

  async created() {
      let { data } = await axios.get(
      'https://server-getdada.herokuapp.com/everydaySuffer'
      )
      this.chartData.rows = data
      data = await axios.get(
      'https://server-getdada.herokuapp.com/totalSuffer'
      )
      this.chartData1.rows= data.data
      data = await axios.get(
      'https://server-getdada.herokuapp.com/death'
      )
      this.chartData2.rows= data.data
      
    
      
  //    this.chartExtend = {
  //     series(item) {
  //       console.log(item)
  //       item[0].data = item[0].data.map((v,index) => ({
          
				
	// 				itemStyle: { color: COLOR_LIST[0] }
	// 			}))
  //        console.log(item)
	// 			return item
  //     }
  //  }
       
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
