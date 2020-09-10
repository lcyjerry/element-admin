<template>
  <el-form
    @submit.native.prevent="onSubmit"
    ref="form"
    :model="article"
    label-width="80px"
  >
    <el-form-item label="活动名称">
      <el-input v-model="article.name"></el-input>
    </el-form-item>

    <el-form-item label="活动形式">
      <el-input type="textarea" v-model="article.desc"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" native-type="submit">立即创建</el-button>
      <el-button>取消</el-button>
    </el-form-item>
  </el-form>
</template>
<script>
export default {
  data() {
    return {
      article: {},
    };
  },
  methods: {
    onSubmit() {
      this.$http.post("articles", this.article).then((res) => {
        this.$message({
          message: "文章创建成功",
          type: "success",
        });
        this.$router.push("/articles/index")
      });
    },
  },
};
</script>
