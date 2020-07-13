<template>
  <div class="container">
    <el-row :gutter="20">
      <el-col :span="4">
        <el-tabs type="border-card">
          <el-tab-pane label="接口">
            <div style="margin-top: 15px;">
              <el-input v-model="searchInterfaceName" placeholder="请输入接口名" class="input-with-select" size="small">
                <el-button slot="append" icon="el-icon-search" size="small" />
              </el-input>
            </div>
            <TeamProjectNavigation @selectedTeamProject="selectedInterfaceTeamProject" />
          </el-tab-pane>
          <el-tab-pane label="套件">
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
          :team="selectInterfaceTeam"
          :project="selectInterfaceProject"
        />
        <SuiteList
          ref="suite"
          :team="selectSuiteTeam"
          :project="selectSuiteProject"
        />
        <div class="grid-content bg-purple-light" />
      </el-col>
    </el-row>
  </div>
</template>

<style scoped>
.container {
  background-color: rgb(244, 244, 245);;
}
</style>

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
      selectSuiteTeam: '',
      selectInterfaceTeam: '',
      selectSuiteProject: '',
      selectInterfaceProject: '',
      searchSuiteName: '',
      searchInterfaceName: ''
    }
  },
  methods: {
    selectedSuiteTeamProject (value) {
      this.selectSuiteTeam = value.team
      this.selectSuiteProject = value.project
      this.$refs.suite.refresh()
    },
    selectedInterfaceTeamProject (value) {
      this.selectInterfaceTeam = value.team
      this.selectInterfaceProject = value.project
      this.$refs.interface.refresh()
    }
  }
}
</script>
