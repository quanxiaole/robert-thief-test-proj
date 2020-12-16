<template>
    <div class="data-view">
        <div class="data-n-view">
            <ve-line :data="chartData" :settings="chartSettings" :events="chartEvents"></ve-line>
            <!-- <div id="myChart" style="height: 400px"> </div> -->
            <hr>
            <div class="action-btns">
              <div class="action-action" v-for="(item, index) in chartData.rows" :key="index"
                  :class="{selectList: index==currentSelect}"
                  style="cursor: pointer"
                  @click="clickOnAction(index)">
                {{item.time}}
              </div>
            </div>
            <div class="json-show">
                <code>{{chartData.rows[currentSelect]}}</code>
            </div>
        </div>
        <div class="conclusion">
            conclusion
        </div>
    </div>
</template>

<script>
var echarts = require('echarts');
import VeLine from 'v-charts/lib/line.common'
export default {
    props: {

    },
    data () {
      this.chartSettings = {
        metrics: ['footprint', 'free'],
        dimension: ['time'],
      }
      let _this = this;
      this.chartEvents = {
        click: function (e) {
          self.name = e.name
          console.log(123, e, e.dataIndex)
          _this.currentSelect = e.dataIndex;
          let btns = document.getElementsByClassName('action-action');
          console.log(123123, btns[_this.currentSelect])
          btns[_this.currentSelect].scrollIntoView();
        }
      }
      return {
        chartData: {
          columns: ['date', 'footprint', 'free', 'growthRate'],
          rows: [
            { 'footprint': 1523, 'time': '01/01(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicka' },
            { 'footprint': 1223, 'time': '01/02(clickb)', 'free': 1523, 'growthRate': 0.345, 'action': 'clickb' },
            { 'footprint': 2123, 'time': '01/03(clickc)', 'free': 1523, 'growthRate': 0.7, 'action': 'clickc' },
            { 'footprint': 4123, 'time': '01/04(clickd)', 'free': 1523, 'growthRate': 0.31, 'action': 'clickd' },
            { 'footprint': 3123, 'time': '01/05(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicke' },
            { 'footprint': 7123, 'time': '01/06(clicka)', 'free': 1523, 'growthRate': 0.65, 'action': 'clickf' },
            { 'footprint': 1523, 'time': '01/07(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicka' },
            { 'footprint': 1223, 'time': '01/08(clickb)', 'free': 1523, 'growthRate': 0.345, 'action': 'clickb' },
            { 'footprint': 2123, 'time': '01/09(clickc)', 'free': 1523, 'growthRate': 0.7, 'action': 'clickc' },
            { 'footprint': 4123, 'time': '01/10(clickd)', 'free': 1523, 'growthRate': 0.31, 'action': 'clickd' },
            { 'footprint': 3123, 'time': '01/11(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicke' },
            { 'footprint': 7123, 'time': '01/12(clicka)', 'free': 1523, 'growthRate': 0.65, 'action': 'clickf' },
            { 'footprint': 1523, 'time': '01/13(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicka' },
            { 'footprint': 1223, 'time': '01/14(clickb)', 'free': 1523, 'growthRate': 0.345, 'action': 'clickb' },
            { 'footprint': 2123, 'time': '01/15(clickc)', 'free': 1523, 'growthRate': 0.7, 'action': 'clickc' },
            { 'footprint': 4123, 'time': '01/16(clickd)', 'free': 1523, 'growthRate': 0.31, 'action': 'clickd' },
            { 'footprint': 3123, 'time': '01/17(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicke' },
            { 'footprint': 7123, 'time': '01/18(clicka)', 'free': 1523, 'growthRate': 0.65, 'action': 'clickf' },
            { 'footprint': 1523, 'time': '01/21(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicka' },
            { 'footprint': 1223, 'time': '01/22(clickb)', 'free': 1523, 'growthRate': 0.345, 'action': 'clickb' },
            { 'footprint': 2123, 'time': '01/23(clickc)', 'free': 1523, 'growthRate': 0.7, 'action': 'clickc' },
            { 'footprint': 4123, 'time': '01/24(clickd)', 'free': 1523, 'growthRate': 0.31, 'action': 'clickd' },
            { 'footprint': 3123, 'time': '01/25(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicke' },
            { 'footprint': 7123, 'time': '01/26(clicka)', 'free': 1523, 'growthRate': 0.65, 'action': 'clickf' },
            { 'footprint': 1523, 'time': '01/27(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicka' },
            { 'footprint': 1223, 'time': '01/28(clickb)', 'free': 1523, 'growthRate': 0.345, 'action': 'clickb' },
            { 'footprint': 2123, 'time': '01/29(clickc)', 'free': 1523, 'growthRate': 0.7, 'action': 'clickc' },
            { 'footprint': 4123, 'time': '01/30(clickd)', 'free': 1523, 'growthRate': 0.31, 'action': 'clickd' },
            { 'footprint': 3123, 'time': '01/31(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicke' },
            { 'footprint': 7123, 'time': '01/32(clicka)', 'free': 1523, 'growthRate': 0.65, 'action': 'clickf' },
            { 'footprint': 1523, 'time': '01/33(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicka' },
            { 'footprint': 1223, 'time': '01/34(clickb)', 'free': 1523, 'growthRate': 0.345, 'action': 'clickb' },
            { 'footprint': 2123, 'time': '01/35(clickc)', 'free': 1523, 'growthRate': 0.7, 'action': 'clickc' },
            { 'footprint': 4123, 'time': '01/36(clickd)', 'free': 1523, 'growthRate': 0.31, 'action': 'clickd' },
            { 'footprint': 3123, 'time': '01/37(clicka)', 'free': 1523, 'growthRate': 0.12, 'action': 'clicke' },
          ]
        },
        currentSelect: 0,
      }
    },
    computed: {

    },
    created() {

    },
    mounted() {
      // 基于准备好的dom，初始化echarts实例
      console.log('echarts', echarts)

      // var myChart = echarts.init(document.getElementById('myChart'));
      // // 绘制图表
      // myChart.setOption({
      //     title: {
      //         text: 'ECharts 入门示例'
      //     },
      //     tooltip: {},
      //     xAxis: {
      //         data: ['衬衫', '羊毛衫', '雪纺衫', '裤子', '高跟鞋', '袜子']
      //     },
      //     yAxis: {},
      //     series: [{
      //         name: '销量',
      //         type: 'bar',
      //         data: [5, 20, 36, 10, 10, 20]
      //     }]
      // });


    var refreshDelay = 1000;

    console.log("aaaaaaaaaaaaaaaaa");


    function refresh() {
      console.log("refresh");
        var xmlhttp = new XMLHttpRequest();
        xmlhttp.onreadystatechange = function() {
            if(xmlhttp.readyState == 4) {
                if(xmlhttp.status == 200) {
                    var scrollTop = document.documentElement.scrollTop;
                    var scrollHeight = document.body.scrollHeight;
                    var screenheight = window.innerHeight;
                    
                    // var contentElement = document.getElementById("content");
                    // contentElement.innerHTML = contentElement.innerHTML + xmlhttp.responseText;
                    setTimeout(refresh, refreshDelay);
                    
                    let json = JSON.parse(xmlhttp.response);
                    console.log(json);
                    
                    if(scrollHeight - screenheight - scrollTop < 100) {
                        window.scrollTo(0, document.body.scrollHeight);
                    }
                }else {
                    setTimeout(refresh, refreshDelay);
                }
            }
        }
        xmlhttp.open("GET", "memoryfetch", true);
        xmlhttp.send();
    }

    refresh();
      
    },
    watch: {

    },
    methods: {
      clickOnAction(index) {
        this.currentSelect = index;
      }
    },
    components: {
        VeLine
    },
};
</script>

<style scoped>
.data-view {
    min-height: 900px;
}
.conclusion {
    margin-left: 620px;
    min-height: 900px;
}
.data-n-view {
    float: left;
    width: 1200px;
    border-right: 2px solid #dddddd;
    min-height: 900px;
}
.action-btns {
    width: 140px;
    height: 300px;
    overflow-y: scroll;
    float: left;
}
.action-action {
    border-bottom: 1px solid #dddddd;
    color: #555555;
    padding: 4px;
}
.json-show {
    margin-left: 180px;
    height: 300px;
}
.selectList {
  background-color: #dddddd;
}

</style>
