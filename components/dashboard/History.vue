<template>
  <div class="history">
    <el-row>
      <el-col :span="18">
        <VeLine :data="chartData" :settings="chartSettings" :extend="extend" width="94%" />
      </el-col>
      <el-col :span="6">
        <el-card class="box-card">
          <div slot="header" class="clearfix">
            <span>本月新增</span>
          </div>
          <div v-for="(v, k) in month" :key="k" class="text item">
            {{ k }}{{ v }}
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import VeLine from 'v-charts/lib/line'

export default {
  components: {
    VeLine
  },
  props: {
    chartData: {
      type: Object,
      default: () => {}
    },
    month: {
      type: Object,
      default: () => {}
    }
  },
  data () {
    return {
      chartSettings: {
        axisSite: { right: ['套件'] },
        yAxisType: ['KMB', 'value']
      },
      extend: {
        series: {
          label: {
            normal: {
              show: true
            }
          }
        }
      }
    }
  }
}
</script>

<style scoped>
.history {
  background-color: #FFFFFF;
  padding-top: 20px;
  padding-bottom: 20px;
  margin-left: -20px;
  margin-right: -20px;
}

.text {
  font-size: 14px;
}

.item {
  margin-bottom: 18px;
}

.clearfix:before,
.clearfix:after {
  display: table;
  content: "";
}
.clearfix:after {
  clear: both
}

.box-card {
  width: 480px;
}
</style>
