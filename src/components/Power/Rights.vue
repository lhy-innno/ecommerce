<template>
<!-- 面包屑导航 -->
    <div>
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>权限管理</el-breadcrumb-item>
            <el-breadcrumb-item>权限列表</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 卡片 -->
        <el-card>
            <div slot="header"></div>
            <div></div>
        </el-card>
        <el-table :data="rightsList" stripe border>
            <el-table-column type="index"></el-table-column>
            <el-table-column label="权限名称" prop="authName"></el-table-column>
            <el-table-column label="路径" prop="path"></el-table-column>
            <el-table-column label="权限等级" prop="level">
              <template v-slot="scope">
                <el-tag v-if="scope.row.level == '0'">一级</el-tag>
                <el-tag type="success" v-else-if="scope.row.level == '1'">二级</el-tag>
                <el-tag type="info" v-else>三级</el-tag>
              </template>
            </el-table-column>
        </el-table>
    </div>
</template>

<script>
export default {
  data () {
    return {
      rightsList: []
    }
  },
  created () {
    this.getRightsList()
  },
  methods: {
    async getRightsList () {
      const { data: res } = await this.$http.get('rights/list')
      if (res.meta.status !== 200) return this.$message.error('请求权限列表失败')
      this.rightsList = res.data
      console.log(this.rightlist)
    }
  }
}
</script>

<style Lang="less" scoped>

</style>
