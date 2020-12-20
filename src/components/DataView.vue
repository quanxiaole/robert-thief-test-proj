<template>
    <div class="vm-view">
      <div class="vm-header">
            <div class="xlsx-input">
              <input type="file" @change="onChange" />
            </div>
            <div class="sid-select">
              <el-select @change="previewSidChange" v-model="currentPreviewSid" filterable placeholder="请选择">
                <el-option
                  v-for="previewSid in previewSessionIds"
                  :key="previewSid"
                  :label="previewSid"
                  :value="previewSid">
                </el-option>
              </el-select>
            </div>
      </div>
      <div class="vm-main">
        <div class="vm-action">
            <ve-line class="vm-chart-area" :data="chartData" :settings="chartSettings" :events="chartEvents"></ve-line>
            <!-- <div id="myChart" style="height: 400px"> </div> -->
            <div class="vm-action-area">
              <div class="action-list">
                <div class="action-action" v-for="(item, index) in chartData.rows" :key="index"
                    :class="{selectList: index==currentSelect}"
                    style="cursor: pointer"
                    @click="clickOnAction(index)">
                  {{`${('000'+(index+1)).slice(-3)} - ${item.time} - ${item.action}`}}
                </div>
              </div>
              <div class="action-json">
                  <textarea>{{pretty(chartData.rows[currentSelect])}}</textarea>
              </div>
            </div>
        </div>
        <div class="vm-info">
          <div class="vm-meta">
            <h1>meta</h1>
            <!-- <xlsx-read :file="file">
              <xlsx-json>
                <template #default="{collection}">
                  <div>
                    {{ collection }}
                  </div>
                </template>
              </xlsx-json>
            </xlsx-read> -->
          </div>
          <div class="vm-conclusion">
            <h1 style="text-align:center">conclusion</h1>
            <br>
            <h3>峰值</h3>
            <div>            
              <label>free: 最小值={{free.min}} MB, 最大值={{free.max}} MB</label>
            </div>
            <div>
              <label>footprint: 最大值={{footprint.max}} MB, 最小值={{footprint.min}} MB</label>
            </div>
            <br>
            <div>
              <h3>free连续递减最多的区间Top3</h3>

              <div v-for="(item, index) in top3Decrease" :key="index"
                  style="cursor: pointer; font-weight:bold"
                  @click="clickFreeDecrease(index)">
                {{`Top${index+1} -  ${item.delta.toFixed(2)} MB`}}
                <div v-for="(action, index) in item.actions" :key="index" style="font-weight:normal " @click="clickTopAction(action.index)">
                  {{`${action.time} -  ${action.action} - ${action.free} MB`}}
                </div>
              </div>
            </div>
            <br>
            <div>
              <h3>footprint连续递增最多的区间Top3</h3>
              <div v-for="(item, index) in top3Increase" :key="index"
                  style="cursor: pointer; font-weight:bold"
                  @click="clickFootprintIncrease(index)">
                {{`Top${index+1} -  ${item.delta.toFixed(2)} MB`}}
                <div v-for="(action, index) in item.actions" :key="index" style="font-weight:normal" @click="clickTopAction(action.index)">
                  {{`${action.time} -  ${action.action} - ${action.footprint} MB`}}
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
var echarts = require('echarts');
var xlsx = require('xlsx');
import VeLine from 'v-charts/lib/line.common'



export default {
    props: {

    },
    data () {

      this.chartSettings = {
        metrics: ['free', 'footprint'],
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
          btns[_this.currentSelect].scrollIntoView({behavior: "smooth"});
        }
      }
      return {
        free: {max:0.0,min:0.0},
        footprint:{max:0.0,min:0.0},
        top3Decrease: [],
        top3Increase: [],
        xlsxData: {},
        currentPreviewSid: "",
        previewSessionIds: [],
        chartData: {
          columns: ['time', 'footprint', 'free', 'action'],
          rows: [
                  {
                    "free": "1949.91",
                    "action": "kActionPreviewInit",
                    "time": "16:58:28",
                    "footprint": "205.13"
                  },
                  {
                    "free": "1908.12",
                    "action": "AddTrailerAction",
                    "time": "16:58:28",
                    "footprint": "213.49"
                  },
                  {
                    "free": "1907.94",
                    "action": "PushStepAction",
                    "time": "16:58:28",
                    "params": {
                      "tip": "init"
                    },
                    "footprint": "213.52"
                  },
                  {
                    "free": "1909.38",
                    "action": "kActionPreviewPing",
                    "time": "16:58:29",
                    "footprint": "213.14"
                  },
                  {
                    "free": "1562.52",
                    "action": "kActionPreviewPing",
                    "time": "16:58:30",
                    "footprint": "311.88"
                  },
                  {
                    "free": "1544.05",
                    "action": "KYTLScrollAction",
                    "time": "16:58:33",
                    "footprint": "348.97"
                  },
                  {
                    "free": "1147.55",
                    "action": "KYTLScrollAction",
                    "time": "16:58:34",
                    "footprint": "379.22"
                  },
                  {
                    "free": "1113.34",
                    "action": "kActionPreviewSeek",
                    "time": "16:58:34",
                    "params": {
                      "comp": {
                        "filter": [
                          {
                            "name": "辞岁",
                            "filterId": "144"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ],
                        "audioAssets": [
                          {
                            "type": 4,
                            "name": "笑纳（DJ版）"
                          }
                        ],
                        "subTrackAssets": [
                          {
                            "materialType": 1
                          },
                          {
                            "materialType": 1
                          }
                        ],
                        "stickerAssets": [
                          {
                            "name": "点赞"
                          }
                        ],
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "videoEffects": [
                          {
                            "resId": "1291",
                            "name": "金粉落下"
                          }
                        ]
                      },
                      "summary": "1trackAsset+2subTrackAssets+1stickerAssets+1videoEffects+1filter+1beauty+1audioAssets",
                      "seek": "4.64"
                    },
                    "footprint": "389.19"
                  }
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

   var _this = this;
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
                    
                    if (xmlhttp.response) {
                      let json = JSON.parse(xmlhttp.response);
                      if (Array.isArray(json)) {
                        for (let i = 0; i < json.length; ++i) {
                          let obj = json[i];
                          obj.time = obj.time;
                          obj.action = obj.act;
                          obj.free = obj.free;
                          obj.footprint = obj.fp;
                          delete obj.fp;
                          obj.params = obj.params;
                        }
                        _this.chartData.rows = json;
                        _this.updateData();
                        console.log(JSON.stringify(json, null, 2))
}                    }
                    
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

    // refresh();

    this.updateData();
      
    },
    watch: {

    },
    // filters: {
    //   pretty: function(value) {
    //     let jsonStr = JSON.stringify(value, null, 2);
    //     console.log(jsonStr);
    //     return jsonStr;
    //   }
    // },
    methods: {
      previewSidChange() {
        this.chartData.rows = this.xlsxData[this.currentPreviewSid];
        this.updateData();
      },

      async onChange (event) {
        let file = event.target.files ? event.target.files[0] : null;
        if (!file) return;
        let dataBinary = await this.readFile(file)
        let workBook = xlsx.read(dataBinary, {type: 'binary', cellDates: true})
        let workSheet = workBook.Sheets[workBook.SheetNames[0]]
        const data = xlsx.utils.sheet_to_json(workSheet)

        if (!data || data.length == 0) return;

        let firstPreviewSid = data[0].preview_sid;

        for (let i = 0; i < data.length; ++i) {
          let item = data[i];
          if (!this.xlsxData.hasOwnProperty(item.preview_sid)) {
            this.xlsxData[item.preview_sid] = [];
          }

          this.xlsxData[item.preview_sid].push({
              free: item.act_free,
              action: item.act_name,
              time: item.act_time,
              footprint: item.act_footprint,
              params: item.act_params,
          });
        }
        this.chartData.rows = this.xlsxData[firstPreviewSid];
        this.previewSessionIds = Object.keys(this.xlsxData);
        this.updateData();
      },

      readFile(file) {
        return new Promise(resolve => {
          let reader = new FileReader()
          reader.readAsBinaryString(file)
          reader.onload = ev => {
            resolve(ev.target.result)
          }
        })
      },

      sortData() {
        let array = [];
        for (let i = 0; i < this.chartData.rows.length; ++i) {
          let row = this.chartData.rows[i];
          let data = {
            time: row.time,
            action: row.action,
            free: row.free,
            footprint: row.footprint,
            params: row.params || {},
          }
          if (!row.params) {
            delete data.params;
          }
          array.push(data);
        }
        this.chartData.rows = array;
      },

      updateData() {
        this.sortData();
        this.countFreeExtreme();
        this.countFootprintExtreme();
        this.decreaseAction();
        this.increaseAction();
      },

      clickOnAction(index) {
        this.currentSelect = index;
      },

      clickTopAction(index) {
        this.currentSelect = index;
        let btns = document.getElementsByClassName('action-action');
        btns[this.currentSelect].scrollIntoView({behavior: "smooth"});
      },

      pretty: function(value) {
        if (!value) return "";
        let jsonStr = JSON.stringify(value, null, 2);
        return jsonStr;
      },

      countFreeExtreme: function() {
        if (!this.chartData.rows) return 0;
        let min = 999999.0;
        let max = 0;
        for (let i = 0; i < this.chartData.rows.length; ++i) {
          let row = this.chartData.rows[i];
          let free = parseFloat(row.free);
          if (free < min) {
            min = free;
          }
          if (free > max) {
            max = free;
          }
        }
        this.free = {
          min: min,
          max: max,
        }
      },

      countFootprintExtreme: function() {
        if (!this.chartData.rows) return 0;
        let min = 999999.0;
        let max = 0;
        for (let i = 0; i < this.chartData.rows.length; ++i) {
          let row = this.chartData.rows[i];
          let footprint = parseFloat(row.footprint);
          if (footprint < min) {
            min = footprint;
          }
          if (footprint > max ) {
            max = footprint;
          }
        }
        this.footprint = {
          min: min,
          max: max,
        }
      },

      increaseAction: function() {
        let res = [];
        let item = {
          actions:[],
          footprintValues:[],
          delta:0.0,
        };
        let prevFootPrint = 0.0;
        for (let i = 0; i < this.chartData.rows.length; ++i) {
          let row = this.chartData.rows[i];
          let footprint = parseFloat(row.footprint);
          if (footprint > prevFootPrint) {
            row.index = i;
            item.actions.push(row);
            item.footprintValues.push(footprint);
          } else {
            // 记录上一段区间
            if (item.actions.length > 1) {
              item.delta = item.footprintValues[item.footprintValues.length-1] - item.footprintValues[0];
              res.push(item);
            }
            item = {
              actions:[],
              footprintValues:[],
              delta:0.0,
            }
            row.index = i;
            item.actions.push(row);
            item.footprintValues.push(footprint);
          }
          prevFootPrint = footprint;
        }

        res.sort(function(a, b) {
          return b.delta - a.delta;
        });

        this.top3Increase = res.slice(0, res.length > 3 ? 3 : res.length);
      },

      decreaseAction: function() {

        let res = [];
        let item = {
          actions:[],
          freeValues:[],
          delta:0.0,
        };
        let prevFree = 99999.0;
        for (let i = 0; i < this.chartData.rows.length; ++i) {
          let row = this.chartData.rows[i];
          let free = parseFloat(row.free);
          if (free < prevFree) {
            row.index = i;
            item.actions.push(row);
            item.freeValues.push(free);
          } else {
            // 记录上一段区间
            if (item.actions.length > 1) {
              item.delta = item.freeValues[0] - item.freeValues[item.freeValues.length-1];
              res.push(item);
            }
            item = {
              actions:[],
              freeValues:[],
              delta:0.0,
            }
            row.index = i;
            item.actions.push(row);
            item.freeValues.push(free);
          }
          prevFree = free;
        }

        res.sort(function(a, b) {
          return b.delta - a.delta;
        });

        this.top3Decrease = res.slice(0, res.length > 3 ? 3 : res.length);
        // console.log(res);
      }

    },
    components: {
        VeLine,
    },
};
</script>

<style scoped>
.vm-view {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100vw;
}

.vm-header {
  flex: 0 0 64px;
  background: lightblue;
  display: flex;
  flex-direction: row;
}

.vm-header .xlsx-input {
  align-self: center;
}

.vm-header .sid-select {
  align-self: center;
}

.vm-main {
  display: flex;
  flex-direction: row;
}

.vm-action {
    display: flex;
    flex-direction: column;
    flex: 0 0 1400px;
    border-right: 2px solid #dddddd;
}

.vm-info {
  display: flex;
  flex: 1;
  flex-direction: column;
  padding: 20px;
  height: calc(100vh - 64px);
  box-sizing: border-box;
  overflow-y: scroll;
}

/*注意：ve-chart若使用display:flex会显示不出来 */
.vm-chart-area {
  flex:0 0 420px;
}

.vm-action-area {
  display: flex;
  flex-basis: calc(100vh - 484px);
  flex-grow: 0;
  flex-shrink: 0;
}

.action-list {
  flex: 3;
  text-align: left;
  overflow-y: scroll;
  height: calc(100vh - 484px);
}

.action-action {
    border-bottom: 1px solid #dddddd;
    color: #555555;
    padding: 4px;
}

.action-json {
  flex: 6;
  background: lightseagreen;
}

.action-json textarea {
  width: 100%;
  height: 100%;
  border: none;
  background:#eeeeee;
  padding: 10px;
  box-sizing: border-box;
  outline: none;
}


.selectList {
  background-color:rgb(190, 229, 205);
}

.vm-meta {
  height: 120px;
  overflow-y: scroll;
  border-bottom: 1px solid #dddddd;
  flex: 0 0 200px
}

.vm-conclusion {
  text-align: left;
  flex: 1;
}


.action-area {
  border-top: 1px solid #dddddd;
  padding: 10px;
  /* height: calc( 100vh - 420px ); */
  /* padding-bottom: 30px; */
  box-sizing: border-box;
}

</style>
