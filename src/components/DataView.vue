<template>
    <div class="data-view">
        <div class="data-n-view">
            <ve-line :data="chartData" :settings="chartSettings"></ve-line>
            <hr>
        </div>
        <div class="conclusion">
            conclusion
        </div>
    </div>
</template>

<script>
import VeLine from 'v-charts/lib/line.common'
export default {
    props: {

    },
    data () {
      this.chartSettings = {
        metrics: ['footprint', 'free'],
        dimension: ['time']
      }
      return {
        chartData: {
          columns: ['date', 'footprint', 'free', 'growthRate'],
          rows: [
            { 'cost': 1523, 'time': '01/01(clicka)', 'profit': 1523, 'growthRate': 0.12, 'action': 'clicka' },
            { 'cost': 1223, 'time': '01/02(clickb)', 'profit': 1523, 'growthRate': 0.345, 'action': 'clickb' },
            { 'cost': 2123, 'time': '01/03(clickc)', 'profit': 1523, 'growthRate': 0.7, 'action': 'clickc' },
            { 'cost': 4123, 'time': '01/04(clickd)', 'profit': 1523, 'growthRate': 0.31, 'action': 'clickd' },
            { 'cost': 3123, 'time': '01/05(clicka)', 'profit': 1523, 'growthRate': 0.12, 'action': 'clicke' },
            { 'cost': 7123, 'time': '01/06(clicka)', 'profit': 1523, 'growthRate': 0.65, 'action': 'clickf' },
          ]
        }
      }
    },
    computed: {

    },
    created() {

    },
    mounted() {

    },
    watch: {

    },
    methods: {

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
</style>
