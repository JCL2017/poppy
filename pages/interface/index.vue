<template>
  <div class="container">
    <el-row :gutter="20">
      <el-col :span="4">
        <el-tabs @tab-click="handleClick" v-model="activeTab" type="border-card">
          <el-tab-pane label="接口" name="interface">
            <div style="margin-top: 15px;">
              <el-input v-model="searchInterfaceName" placeholder="请输入接口名" class="input-with-select" size="small">
                <el-button slot="append" icon="el-icon-search" size="small" />
              </el-input>
            </div>
            <TeamProjectNavigation @selectedTeamProject="selectedInterfaceTeamProject" />
          </el-tab-pane>
          <el-tab-pane label="套件" name="suite">
            <div style="margin-top: 15px;">
              <el-input v-model="searchSuiteName" placeholder="请输入套件名" class="input-with-select" size="small">
                <el-button slot="append" icon="el-icon-search" size="small" />
              </el-input>
            </div>
            <TeamProjectNavigation @selectedTeamProject="selectedSuiteTeamProject" />
          </el-tab-pane>
        </el-tabs>
      </el-col>
      <el-col :span="20">
        <InterfaceList
          ref="interface"
          v-show="this.switch === true"
        />
        <SuiteList
          ref="suite"
          v-show="this.switch === false"
        />
        <div class="grid-content bg-purple-light" />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import SuiteList from '~/components/SuiteList.vue'
import InterfaceList from '~/components/InterfaceList.vue'
import TeamProjectNavigation from '~/components/TeamProjectNavigation.vue'

export default {
  components: {
    SuiteList,
    InterfaceList,
    TeamProjectNavigation
  },
  data () {
    return {
      switch: true,
      activeTab: 'interface',
      searchSuiteName: '',
      searchInterfaceName: '',
      interface: {
        team: '',
        project: ''
      },
      suite: {
        team: '',
        project: ''
      }
    }
  },
  mounted () {
    // 当创建套件后跳转会携带type属性，否则认为是刷新接口列表
    if (this.$route.query.tab === 'suite') {
      this.activeTab = 'suite'
      this.$refs.suite.refresh({
        team: this.suite.team,
        project: this.suite.project
      })
    } else {
      this.$refs.interface.refresh({
        team: this.interface.team,
        project: this.interface.project
      })
    }
  },
  methods: {
    handleClick (tab, event) {
      if (tab.name === 'interface') {
        this.switch = true
        this.activeTab = 'interface'
        this.$refs.interface.refresh({
          team: this.interface.team,
          project: this.interface.project
        })
      } else {
        this.switch = false
        this.activeTab = 'suite'
        this.$refs.suite.refresh({
          team: this.suite.team,
          project: this.suite.project
        })
      }
    },
    selectedInterfaceTeamProject (value) {
      this.interface.team = value.team
      this.interface.project = value.project
      this.$refs.interface.refresh({
        team: this.interface.team,
        project: this.interface.project
      })
    },
    selectedSuiteTeamProject (value) {
      this.suite.team = value.team
      this.suite.project = value.project
      this.$refs.suite.refresh({
        team: this.suite.team,
        project: this.suite.project
      })
    }
  }
}
</script>
