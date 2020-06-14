<template>
  <div class="banner">
    <el-row>
      <el-col :span="4" v-for="item in summary" :key="item.description">
        <el-row class="card">
          <el-col :span="8" :style="{background: item.color}" class="icon">
            <i :class="item.icon" />
          </el-col>
          <el-col :span="16" class="content">
            <div><span class="number">{{ item.number }}</span></div>
            <div><span class="description">{{ item.description }}</span></div>
          </el-col>
        </el-row>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  props: {
    summary: {
      type: Object,
      default: () => {}
    }
  }
}
</script>

<style scoped>
.banner {
  background-color: #F2F2F2;
  padding-top: 20px;
  padding-bottom: 20px;
  margin-left: -20px;
  margin-right: -20px;
}

.card {
  padding-left: 10px;
  padding-right: 10px;
}

.icon {
  height: 100px;
  font-size: 24px;
  border-radius: 5px 0 0 5px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.content {
  border-radius: 0 5px 5px 0;
  background-color: #FFFFFF;
}

.number {
  font-size: 48px;
  line-height: 70px;
  width: 100%;
  text-align: center;
  display: inline-block;
}

.description {
  font-size: 14px;
  line-height: 30px;
  width: 100%;
  text-align: center;
  display: inline-block;
  background-color: #FFFFFF;
}
</style>
