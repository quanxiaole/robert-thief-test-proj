<template>
    <div class="data-view">
        <div class="data-n-view">
            <ve-line :data="chartData" :settings="chartSettings" :events="chartEvents"></ve-line>
            <div id="myChart" style="height: 400px"> </div>
            <hr>
            <div class="action-btns">
              <div class="action-action" v-for="(item, index) in chartData.rows" :key="index"
                  :class="{selectList: index==currentSelect}"
                  style="cursor: pointer"
                  @click="clickOnAction(index)">
                {{`${('000'+(index+1)).slice(-3)} - ${item.time} - ${item.act}`}}
              </div>
            </div>
            <div class="json-show">
                <textarea style="width:400px;height:500px">{{pretty(chartData.rows[currentSelect])}}</textarea>
            </div>
        </div>
        <div class="conclusion">
            <label>conclusion</label>
            <div>            
              <label>free最小值:{{freeMinValue()}}MB</label>
            </div>
            <div>
              <label>footprint最大值:{{footprintMaxValue()}}MB</label>
            </div>
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
      myChart: {}
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
          btns[_this.currentSelect].scrollIntoView();
        }
      }
      return {
        chartData: {
          columns: ['time', 'footprint', 'free', 'act'],
          rows: [
                  {
                    "free": "1949.91",
                    "act": "kActionPreviewInit",
                    "time": "16:58:28",
                    "footprint": "205.13"
                  },
                  {
                    "free": "1908.12",
                    "act": "AddTrailerAction",
                    "time": "16:58:28",
                    "footprint": "213.49"
                  },
                  {
                    "free": "1907.94",
                    "act": "PushStepAction",
                    "time": "16:58:28",
                    "params": {
                      "tip": "init"
                    },
                    "footprint": "213.52"
                  },
                  {
                    "free": "1909.38",
                    "act": "kActionPreviewPing",
                    "time": "16:58:29",
                    "footprint": "213.14"
                  },
                  {
                    "free": "1562.52",
                    "act": "kActionPreviewPing",
                    "time": "16:58:30",
                    "footprint": "311.88"
                  },
                  {
                    "free": "1544.05",
                    "act": "KYTLScrollAction",
                    "time": "16:58:33",
                    "footprint": "348.97"
                  },
                  {
                    "free": "1147.55",
                    "act": "KYTLScrollAction",
                    "time": "16:58:34",
                    "footprint": "379.22"
                  },
                  {
                    "free": "1113.34",
                    "act": "kActionPreviewSeek",
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
                  },
                  {
                    "free": "1018.00",
                    "act": "KYTLScrollAction",
                    "time": "16:58:35",
                    "footprint": "442.97"
                  },
                  {
                    "free": "1355.27",
                    "act": "kActionPreviewSeek",
                    "time": "16:58:35",
                    "params": {
                      "comp": {
                        "audioAssets": [
                          {
                            "type": 4,
                            "name": "笑纳（DJ版）"
                          }
                        ],
                        "videoEffects": [
                          {
                            "resId": "1291",
                            "name": "金粉落下"
                          }
                        ],
                        "filter": [
                          {
                            "name": "辞岁",
                            "filterId": "144"
                          }
                        ],
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "stickerAssets": [
                          {
                            "name": "点赞"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1stickerAssets+1videoEffects+1filter+1beauty+1audioAssets",
                      "seek": "4.22"
                    },
                    "footprint": "471.64"
                  },
                  {
                    "free": "1291.95",
                    "act": "BottomTabChangeAction",
                    "time": "16:58:36",
                    "params": {
                      "name": "MATERIAL"
                    },
                    "footprint": "472.08"
                  },
                  {
                    "free": "1211.44",
                    "act": "BottomTabChangeAction",
                    "time": "16:58:37",
                    "params": {
                      "name": "AUDIO"
                    },
                    "footprint": "444.16"
                  },
                  {
                    "free": "1303.08",
                    "act": "BottomTabChangeAction",
                    "time": "16:58:38",
                    "params": {
                      "name": "AUDIO"
                    },
                    "footprint": "443.02"
                  },
                  {
                    "free": "1336.02",
                    "act": "BottomTabChangeAction",
                    "time": "16:58:39",
                    "params": {
                      "name": "MATERIAL"
                    },
                    "footprint": "443.02"
                  },
                  {
                    "free": "1364.25",
                    "act": "PopWindowChange",
                    "time": "16:58:39",
                    "params": {
                      "type": "STICKER"
                    },
                    "footprint": "443.46"
                  },
                  {
                    "free": "1314.52",
                    "act": "kActionPreviewPing",
                    "time": "16:58:40",
                    "footprint": "450.31"
                  },
                  {
                    "free": "1299.78",
                    "act": "PopWindowChange",
                    "time": "16:58:41",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "453.64"
                  },
                  {
                    "free": "1314.17",
                    "act": "PopWindowChange",
                    "time": "16:58:42",
                    "params": {
                      "type": "CUSTOM_STICKER"
                    },
                    "footprint": "453.55"
                  },
                  {
                    "free": "1287.11",
                    "act": "PopWindowChange",
                    "time": "16:58:43",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "459.69"
                  },
                  {
                    "free": "1309.25",
                    "act": "kActionPreviewBtnExportSetting",
                    "time": "16:58:44",
                    "footprint": "458.05"
                  },
                  {
                    "free": "1301.22",
                    "act": "kActionPreviewPing",
                    "time": "16:58:45",
                    "footprint": "457.56"
                  },
                  {
                    "free": "1312.00",
                    "act": "kActionPreviewBtnPlay",
                    "time": "16:58:46",
                    "footprint": "457.41"
                  },
                  {
                    "free": "1262.03",
                    "act": "kActionPreviewPing",
                    "time": "16:58:47",
                    "footprint": "474.39"
                  },
                  {
                    "free": "1263.38",
                    "act": "kActionPreviewBtnPause",
                    "time": "16:58:48",
                    "footprint": "474.50"
                  },
                  {
                    "free": "1265.39",
                    "act": "KYTLScrollAction",
                    "time": "16:58:48",
                    "footprint": "472.24"
                  },
                  {
                    "free": "1132.78",
                    "act": "KYTLScrollAction",
                    "time": "16:58:49",
                    "footprint": "492.00"
                  },
                  {
                    "free": "1148.89",
                    "act": "kActionPreviewSeek",
                    "time": "16:58:49",
                    "params": {
                      "comp": {
                        "filter": [
                          {
                            "name": "辞岁",
                            "filterId": "144"
                          }
                        ],
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ],
                        "subtitleStickerAssets": [
                          {
                            "type": "sticker_type_subtitle",
                            "name": "请输入文本"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1filter+1beauty+1subtitleStickerAssets",
                      "seek": "2.06"
                    },
                    "footprint": "464.47"
                  },
                  {
                    "free": "1191.64",
                    "act": "BottomTabChangeAction",
                    "time": "16:58:50",
                    "params": {
                      "name": "ADJUST"
                    },
                    "footprint": "476.41"
                  },
                  {
                    "free": "1270.56",
                    "act": "PopWindowChange",
                    "time": "16:58:51",
                    "params": {
                      "type": "VIDEO_EFFECT"
                    },
                    "footprint": "476.33"
                  },
                  {
                    "free": "1264.17",
                    "act": "PopWindowChange",
                    "time": "16:58:52",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "498.41"
                  },
                  {
                    "free": "1288.22",
                    "act": "kActionPreviewPing",
                    "time": "16:58:53",
                    "footprint": "460.05"
                  },
                  {
                    "free": "1288.45",
                    "act": "PopWindowChange",
                    "time": "16:58:53",
                    "params": {
                      "type": "BEAUTY"
                    },
                    "footprint": "460.05"
                  },
                  {
                    "free": "1298.20",
                    "act": "kActionPreviewPing",
                    "time": "16:58:54",
                    "footprint": "459.58"
                  },
                  {
                    "free": "1292.06",
                    "act": "SetBeautyAction",
                    "time": "16:58:55",
                    "params": {
                      "type": "-1"
                    },
                    "footprint": "460.06"
                  },
                  {
                    "free": "1277.88",
                    "act": "PushStepAction",
                    "time": "16:58:55",
                    "params": {
                      "tip": "美颜"
                    },
                    "footprint": "459.97"
                  },
                  {
                    "free": "1278.22",
                    "act": "PopWindowChange",
                    "time": "16:58:55",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "459.88"
                  },
                  {
                    "free": "1276.00",
                    "act": "PopWindowChange",
                    "time": "16:58:56",
                    "params": {
                      "type": "FILTER"
                    },
                    "footprint": "459.35"
                  },
                  {
                    "free": "1266.34",
                    "act": "SetFilterAction",
                    "time": "16:58:56",
                    "params": {
                      "name": "辞岁",
                      "id": "辞岁",
                      "type": "2"
                    },
                    "footprint": "459.83"
                  },
                  {
                    "free": "1272.33",
                    "act": "SetFilterAction",
                    "time": "16:58:57",
                    "params": {
                      "name": "白嫩",
                      "id": "白嫩",
                      "type": "2"
                    },
                    "footprint": "459.86"
                  },
                  {
                    "free": "1277.39",
                    "act": "PushStepAction",
                    "time": "16:58:58",
                    "params": {
                      "tip": "滤镜"
                    },
                    "footprint": "461.14"
                  },
                  {
                    "free": "1277.61",
                    "act": "PopWindowChange",
                    "time": "16:58:58",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "461.10"
                  },
                  {
                    "free": "1276.30",
                    "act": "BottomTabChangeAction",
                    "time": "16:58:59",
                    "params": {
                      "name": "AUDIO"
                    },
                    "footprint": "459.33"
                  },
                  {
                    "free": "1279.53",
                    "act": "kActionPreviewPing",
                    "time": "16:59:00",
                    "footprint": "458.42"
                  },
                  {
                    "free": "1275.89",
                    "act": "kActionPreviewPing",
                    "time": "16:59:01",
                    "footprint": "457.91"
                  },
                  {
                    "free": "1280.20",
                    "act": "BottomTabChangeAction",
                    "time": "16:59:02",
                    "params": {
                      "name": "SUBTITLE"
                    },
                    "footprint": "455.97"
                  },
                  {
                    "free": "1269.53",
                    "act": "KYTLScrollAction",
                    "time": "16:59:03",
                    "footprint": "449.61"
                  },
                  {
                    "free": "1489.56",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:03",
                    "params": {
                      "comp": {
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
                          }
                        ],
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ],
                        "subtitleStickerAssets": [
                          {
                            "type": "sticker_type_subtitle",
                            "name": "请输入文本"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1filter+1beauty+1subtitleStickerAssets",
                      "seek": "1.90"
                    },
                    "footprint": "479.03"
                  },
                  {
                    "free": "1415.47",
                    "act": "KYTLSegmentTapAction",
                    "time": "16:59:03",
                    "footprint": "486.64"
                  },
                  {
                    "free": "1303.12",
                    "act": "KYTLSegmentDragHolderAction",
                    "time": "16:59:04",
                    "footprint": "491.07"
                  },
                  {
                    "free": "1303.23",
                    "act": "CommandAction",
                    "time": "16:59:04",
                    "footprint": "491.08"
                  },
                  {
                    "free": "1307.03",
                    "act": "KYTLSegmentDragHolderAction",
                    "time": "16:59:05",
                    "footprint": "486.69"
                  },
                  {
                    "free": "1306.72",
                    "act": "CommandAction",
                    "time": "16:59:05",
                    "footprint": "486.72"
                  },
                  {
                    "free": "1293.23",
                    "act": "SelectedSegmentChangeAction",
                    "time": "16:59:05",
                    "footprint": "491.88"
                  },
                  {
                    "free": "1407.56",
                    "act": "KYTLScrollAction",
                    "time": "16:59:06",
                    "footprint": "487.53"
                  },
                  {
                    "free": "1416.88",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:06",
                    "params": {
                      "comp": {
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1filter+1beauty",
                      "seek": "0.00"
                    },
                    "footprint": "480.61"
                  },
                  {
                    "free": "1284.53",
                    "act": "BottomTabChangeAction",
                    "time": "16:59:06",
                    "params": {
                      "name": "MATERIAL"
                    },
                    "footprint": "460.86"
                  },
                  {
                    "free": "1254.50",
                    "act": "BottomTabChangeAction",
                    "time": "16:59:07",
                    "params": {
                      "name": "TRIM"
                    },
                    "footprint": "444.36"
                  },
                  {
                    "free": "1086.83",
                    "act": "KYTLScrollAction",
                    "time": "16:59:07",
                    "footprint": "463.19"
                  },
                  {
                    "free": "1078.44",
                    "act": "KYTLScrollAction",
                    "time": "16:59:08",
                    "footprint": "457.55"
                  },
                  {
                    "free": "1031.03",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:08",
                    "params": {
                      "comp": {
                        "videoEffects": [
                          {
                            "resId": "1291",
                            "name": "金粉落下"
                          }
                        ],
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
                          }
                        ],
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ],
                        "subtitleStickerAssets": [
                          {
                            "type": "sticker_type_subtitle",
                            "name": "请输入文本"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1videoEffects+1filter+1beauty+1subtitleStickerAssets",
                      "seek": "2.56"
                    },
                    "footprint": "481.83"
                  },
                  {
                    "free": "1140.28",
                    "act": "PopWindowChange",
                    "time": "16:59:08",
                    "params": {
                      "type": "BACKGROUND"
                    },
                    "footprint": "480.75"
                  },
                  {
                    "free": "1176.47",
                    "act": "kActionPreviewPing",
                    "time": "16:59:09",
                    "footprint": "514.28"
                  },
                  {
                    "free": "1229.27",
                    "act": "PopWindowChange",
                    "time": "16:59:10",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "499.35"
                  },
                  {
                    "free": "1237.53",
                    "act": "kActionPreviewPing",
                    "time": "16:59:11",
                    "footprint": "503.25"
                  },
                  {
                    "free": "1230.36",
                    "act": "kActionPreviewPing",
                    "time": "16:59:12",
                    "footprint": "509.53"
                  },
                  {
                    "free": "1227.31",
                    "act": "AddTrackEffectAction",
                    "time": "16:59:13",
                    "params": {
                      "name": "逐渐抖入",
                      "type": "0",
                      "res_id": "6595"
                    },
                    "footprint": "512.13"
                  },
                  {
                    "free": "1184.05",
                    "act": "PushStepAction",
                    "time": "16:59:13",
                    "params": {
                      "tip": "动画 调整"
                    },
                    "footprint": "508.44"
                  },
                  {
                    "free": "1180.05",
                    "act": "PopWindowChange",
                    "time": "16:59:13",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "508.44"
                  },
                  {
                    "free": "1215.27",
                    "act": "KYTLScrollAction",
                    "time": "16:59:14",
                    "footprint": "487.36"
                  },
                  {
                    "free": "1198.45",
                    "act": "KYTLScrollAction",
                    "time": "16:59:15",
                    "footprint": "501.78"
                  },
                  {
                    "free": "1435.34",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:15",
                    "params": {
                      "comp": {
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
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
                        "stickerAssets": [
                          {
                            "name": "点赞"
                          }
                        ],
                        "subtitleStickerAssets": [
                          {
                            "type": "sticker_type_subtitle",
                            "name": "请输入文本"
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
                      "summary": "1trackAsset+1stickerAssets+1videoEffects+1filter+1beauty+1audioAssets+1subtitleStickerAssets",
                      "seek": "3.96"
                    },
                    "footprint": "508.80"
                  },
                  {
                    "free": "1400.31",
                    "act": "SplitVideoAction",
                    "time": "16:59:16",
                    "footprint": "465.39"
                  },
                  {
                    "free": "1428.11",
                    "act": "kActionPreviewPing",
                    "time": "16:59:17",
                    "footprint": "493.36"
                  },
                  {
                    "free": "1475.44",
                    "act": "kActionPreviewPing",
                    "time": "16:59:18",
                    "footprint": "493.38"
                  },
                  {
                    "free": "1561.67",
                    "act": "CopyVideoAction",
                    "time": "16:59:20",
                    "footprint": "473.97"
                  },
                  {
                    "free": "1115.73",
                    "act": "kActionPreviewPing",
                    "time": "16:59:21",
                    "footprint": "506.89"
                  },
                  {
                    "free": "1389.11",
                    "act": "kActionPreviewPing",
                    "time": "16:59:22",
                    "footprint": "506.89"
                  },
                  {
                    "free": "1402.77",
                    "act": "PopWindowChange",
                    "time": "16:59:25",
                    "params": {
                      "type": "TRACK_ORDER"
                    },
                    "footprint": "506.49"
                  },
                  {
                    "free": "1340.48",
                    "act": "PopWindowChange",
                    "time": "16:59:26",
                    "params": {
                      "type": "null"
                    },
                    "footprint": "509.08"
                  },
                  {
                    "free": "1340.52",
                    "act": "UpdateOrderAction",
                    "time": "16:59:26",
                    "footprint": "509.08"
                  },
                  {
                    "free": "1306.56",
                    "act": "BottomTabChangeAction",
                    "time": "16:59:27",
                    "params": {
                      "name": "SUBTITLE"
                    },
                    "footprint": "507.53"
                  },
                  {
                    "free": "1381.11",
                    "act": "kActionPreviewPing",
                    "time": "16:59:28",
                    "footprint": "507.35"
                  },
                  {
                    "free": "1383.78",
                    "act": "KYTLScrollAction",
                    "time": "16:59:29",
                    "footprint": "477.38"
                  },
                  {
                    "free": "1383.78",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:29",
                    "params": {
                      "comp": {
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
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
                        "stickerAssets": [
                          {
                            "name": "点赞"
                          }
                        ],
                        "subtitleStickerAssets": [
                          {
                            "type": "sticker_type_subtitle",
                            "name": "请输入文本"
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
                      "summary": "1trackAsset+1stickerAssets+1videoEffects+1filter+1beauty+1audioAssets+1subtitleStickerAssets",
                      "seek": "3.86"
                    },
                    "footprint": "521.08"
                  },
                  {
                    "free": "1466.25",
                    "act": "kActionPreviewPing",
                    "time": "16:59:30",
                    "footprint": "500.96"
                  },
                  {
                    "free": "1486.41",
                    "act": "kActionPreviewPing",
                    "time": "16:59:31",
                    "footprint": "497.75"
                  },
                  {
                    "free": "1507.92",
                    "act": "KYTLScrollAction",
                    "time": "16:59:39",
                    "footprint": "465.27"
                  },
                  {
                    "free": "1021.83",
                    "act": "KYTLScrollAction",
                    "time": "16:59:40",
                    "footprint": "515.67"
                  },
                  {
                    "free": "1021.86",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:40",
                    "params": {
                      "comp": {
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1filter+1beauty",
                      "seek": "1.81"
                    },
                    "footprint": "515.67"
                  },
                  {
                    "free": "1043.23",
                    "act": "RevokeAction",
                    "time": "16:59:41",
                    "footprint": "515.64"
                  },
                  {
                    "free": "1445.78",
                    "act": "kActionPreviewPing",
                    "time": "16:59:42",
                    "footprint": "507.10"
                  },
                  {
                    "free": "1450.33",
                    "act": "RevokeAction",
                    "time": "16:59:43",
                    "footprint": "507.10"
                  },
                  {
                    "free": "1413.39",
                    "act": "KYTLScrollAction",
                    "time": "16:59:44",
                    "footprint": "490.13"
                  },
                  {
                    "free": "1320.95",
                    "act": "KYTLScrollAction",
                    "time": "16:59:45",
                    "footprint": "546.10"
                  },
                  {
                    "free": "1320.95",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:45",
                    "params": {
                      "comp": {
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1filter+1beauty",
                      "seek": "2.01"
                    },
                    "footprint": "546.10"
                  },
                  {
                    "free": "1116.86",
                    "act": "BottomTabChangeAction",
                    "time": "16:59:45",
                    "params": {
                      "name": "MATERIAL"
                    },
                    "footprint": "512.14"
                  },
                  {
                    "free": "1370.64",
                    "act": "kActionPreviewPing",
                    "time": "16:59:46",
                    "footprint": "512.16"
                  },
                  {
                    "free": "1373.05",
                    "act": "BottomTabChangeAction",
                    "time": "16:59:47",
                    "params": {
                      "name": "TRIM"
                    },
                    "footprint": "512.19"
                  },
                  {
                    "free": "1384.91",
                    "act": "KYTLScrollAction",
                    "time": "16:59:47",
                    "footprint": "510.97"
                  },
                  {
                    "free": "1443.69",
                    "act": "KYTLScrollAction",
                    "time": "16:59:48",
                    "footprint": "471.83"
                  },
                  {
                    "free": "1552.48",
                    "act": "KYTLScrollAction",
                    "time": "16:59:49",
                    "footprint": "506.44"
                  },
                  {
                    "free": "1405.66",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:49",
                    "params": {
                      "comp": {
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1filter+1beauty",
                      "seek": "0.43"
                    },
                    "footprint": "485.17"
                  },
                  {
                    "free": "1343.42",
                    "act": "kActionPreviewBtnPlay",
                    "time": "16:59:49",
                    "footprint": "530.91"
                  },
                  {
                    "free": "1735.89",
                    "act": "kActionPreviewPing",
                    "time": "16:59:50",
                    "footprint": "488.61"
                  },
                  {
                    "free": "1730.86",
                    "act": "kActionPreviewBtnPause",
                    "time": "16:59:51",
                    "footprint": "508.80"
                  },
                  {
                    "free": "1549.66",
                    "act": "KYTLScrollAction",
                    "time": "16:59:51",
                    "footprint": "492.41"
                  },
                  {
                    "free": "1564.38",
                    "act": "KYTLScrollAction",
                    "time": "16:59:52",
                    "footprint": "515.88"
                  },
                  {
                    "free": "1345.20",
                    "act": "kActionPreviewSeek",
                    "time": "16:59:52",
                    "params": {
                      "comp": {
                        "trackAsset": [
                          {
                            "background_category": "IMAGE",
                            "background_image": "2F6E6651-4E80-4BF8-9CA5-4B739A070DAE"
                          }
                        ],
                        "filter": [
                          {
                            "name": "水润",
                            "filterId": "104"
                          }
                        ],
                        "beauty": [
                          {
                            "beautyId": "-1"
                          }
                        ]
                      },
                      "summary": "1trackAsset+1filter+1beauty",
                      "seek": "0.67"
                    },
                    "footprint": "508.21"
                  },
                  {
                    "free": "1488.66",
                    "act": "kActionPreviewPing",
                    "time": "16:59:53",
                    "footprint": "466.11"
                  },
                  {
                    "free": "1594.05",
                    "act": "kActionPreviewPing",
                    "time": "16:59:54",
                    "footprint": "466.11"
                  }
                ]
        },
        currentSelect: 0,
      }
    },
    computed: {
      chartDataTime() {
        let res = [];
        for(let i=0; i<this.chartData.rows.length; i++) {
          res.push(this.chartData.rows[i].time)
        }
        console.log('time', res)
        return res;
      },
      chartDataSeries() {
        let freeData = [];
        let footData = [];
        for(let i=0; i<this.chartData.rows.length; i++) {
          freeData.push(parseFloat(this.chartData.rows[i].free))
          footData.push(parseFloat(this.chartData.rows[i].footprint))
        }

        let res = [
          {
            name: 'free',
            type: 'line',
            data: freeData
          },{
            name: 'footprint',
            type: 'line',
            data: footData
          }
        ];
        console.log('data', res)
        return res;
      }
    },
    created() {

    },
    mounted() {
      // 基于准备好的dom，初始化echarts实例
      console.log('echarts', echarts)

      this.myChart = echarts.init(document.getElementById('myChart'));
      // 绘制图表
      this.myChart.setOption({
          title: {
              text: 'ECharts 入门示例'
          },
          tooltip: {},
          xAxis: {
              type: 'category',
              data: this.chartDataTime || ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'] // 时间列表
          },
          yAxis: {
              type: 'value'
          },
          // series: [{
          //     data: this.chartDataSeries || [820, 932, 901, 934, 1290, 1330, 1320], // 数据列表
          //     type: 'line',
          //     smooth: true
          // }]
          series: this.chartDataSeries
      });


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
                          obj.footprint = obj.fp;
                          delete obj.fp;
                        }
                        _this.chartData.rows = json;

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
      clickOnAction(index) {
        this.currentSelect = index;
        this.myChart.dispatchAction({ 
            type: 'highlight',
            dataIndex: index
        })
        this.myChart.dispatchAction({
            type: 'showTip',
            // 系列的 index，在 tooltip 的 trigger 为 axis 的时候可选。
            dataIndex: index,
            position: ['50%', '50%'],
        })
      },

      pretty: function(value) {
        if (!value) return "";
        let jsonStr = JSON.stringify(value, null, 2);
        return jsonStr;
      },

      freeMinValue:function() {
        return 303.12;
      },

      footprintMaxValue:function() {
        return 712.98;
      }

    },
    components: {
        VeLine,
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
    text-align: left;
    width: 360px;
    height: 530px;
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
