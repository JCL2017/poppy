<template>
  <div>
    <Banner :summary="summary" />
    <History :chartData="chartData" :month="month" />
  </div>
</template>

<script>
import Banner from '~/components/dashboard/Banner.vue'
import History from '~/components/dashboard/History.vue'

export default {
  components: {
    Banner,
    History
  },
  data () {
    return {
      summary: {
        team: {
          'number': 0,
          'description': '团队数量',
          'icon': 'el-icon-office-building',
          'color': '#FDE9D9'
        },
        project: {
          'number': 0,
          'description': '项目数量',
          'icon': 'el-icon-s-custom',
          'color': '#DAEEF3'
        },
        interface: {
          'number': 0,
          'description': '接口数量',
          'icon': 'el-icon-s-ticket',
          'color': '#C6D9F1'
        },
        suite: {
          'number': 0,
          'description': '套件数量',
          'icon': 'el-icon-s-grid',
          'color': '#DDD9C3'
        },
        variable: {
          'number': 0,
          'description': '变量数量',
          'icon': 'el-icon-s-flag',
          'color': '#F2DBDB'
        },
        keyword: {
          'number': 0,
          'description': '关键字数量',
          'icon': 'el-icon-s-promotion',
          'color': '#EAF1DD'
        }
      },
      chartData: {
        columns: ['月份', '接口', '套件'],
        rows: []
      },
      month: {
        '接口': 0,
        '套件': 0,
        '变量': 0,
        '关键字': 0
      },
      suite: {}
    }
  },
  mounted () {
    this.count()
  },
  methods: {
    count () {
      this.$axios({
        url: '/api/v1/dashboard/info',
        method: 'post',
        data: JSON.stringify({}),
        headers: {
          'Content-Type': 'application/json;'
        }
      }).then((res) => {
        if (res.data.status === 0) {
          // this.data = res.data.data
          for (const i in res.data.data.summary) {
            this.summary[i].number = res.data.data.summary[i]
          }
          for (const i in res.data.data.history) {
            this.chartData.rows.push({
              '月份': i,
              '接口': res.data.data.history[i].interface,
              '套件': res.data.data.history[i].suite
            })
          }
          for (const i in res.data.data.latest) {
            if (i === 'interface') {
              this.month.接口 = res.data.data.latest[i]
            }
            if (i === 'suite') {
              this.month.套件 = res.data.data.latest[i]
            }
            if (i === 'variable') {
              this.month.变量 = res.data.data.latest[i]
            }
            if (i === 'keyword') {
              this.month.关键字 = res.data.data.latest[i]
            }
          }
        } else {
          this.$message({
            type: 'error',
            message: res.data.message,
            center: true
          })
        }
      }).catch((res) => {
        this.$message({
          type: 'error',
          message: '服务异常，请联系管理员！',
          center: true
        })
      })
    }
  }
}
</script>
