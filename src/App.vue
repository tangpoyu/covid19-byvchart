<template>
  
  <div id="app">
      
      <h1>COVID-19 Tracking Dashboard of Taiwan</h1>
      <ve-line :data="chartData" :colors="color"></ve-line>
      <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/v-charts/lib/style.min.css">
  </div>
  
</template>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/v-charts/lib/index.min.js"></script>
<style>

#app {
    background-color: rgba(241, 236, 156, 0.445);
    
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
          chartData: {
            columns: ['日期', '確診人數'],
            rows: [
             
            ]
          },
          
          color:['#FFD700']
        }
  },

  async created() {
      let { data } = await axios.get(
        'https://covid-19.nchc.org.tw/myDT_staff.php?TB_name=owl_world&limitColumn=a01&limitValue=TW%&equalValue=%20like%20&encodeKey=MTYzMzM1Njc4MA==&c[]=id&t[]=int&d[]=NO&c[]=a01&t[]=varchar&d[]=NO&c[]=a02&t[]=varchar&d[]=NO&c[]=a03&t[]=varchar&d[]=NO&c[]=a04&t[]=date&d[]=NO&c[]=a05&t[]=int&d[]=NO&c[]=a06&t[]=int&d[]=NO&c[]=a07&t[]=decimal&d[]=NO&c[]=a08&t[]=int&d[]=NO&c[]=a09&t[]=int&d[]=NO&c[]=a10&t[]=decimal&d[]=NO&c[]=a11&t[]=decimal&d[]=NO&c[]=a12&t[]=decimal&d[]=NO&c[]=a13&t[]=decimal&d[]=NO&c[]=a14&t[]=int&d[]=NO&c[]=a15&t[]=int&d[]=NO&c[]=a16&t[]=decimal&d[]=NO&c[]=a17&t[]=decimal&d[]=NO&c[]=a18&t[]=decimal&d[]=NO&c[]=a19&t[]=decimal&d[]=NO&c[]=a20&t[]=int&d[]=NO&c[]=a21&t[]=int&d[]=NO&c[]=a22&t[]=int&d[]=NO&c[]=a23&t[]=decimal&d[]=NO&c[]=a24&t[]=decimal&d[]=NO&c[]=a25&t[]=decimal&d[]=NO&c[]=a26&t[]=decimal&d[]=NO&c[]=a27&t[]=int&d[]=NO&c[]=a28&t[]=decimal&d[]=NO&c[]=a29&t[]=decimal&d[]=NO&c[]=a30&t[]=decimal&d[]=NO&c[]=a31&t[]=int&d[]=NO&c[]=a32&t[]=decimal&d[]=NO'
      )
      data=data.data.slice(data.data.length-30)
      console.log(data)

       data.forEach((item) => {
      const date=item.a04
      const{
      a06
      } = item
      this.chartData.rows.push({"日期":date, "確診人數": a06})
      
    })
    console.log(this.chartData.rows)
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
        console.log(this.chartData.rows[0].確診人數)
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
