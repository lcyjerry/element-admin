<template>
  <el-form @submit.native.prevent="saveArticle" ref="form" :model="article" label-width="80px">
    <el-form-item label="活动名称">
      <el-input v-model="article.name"></el-input>
    </el-form-item>

    <el-form-item label="活动形式">
      <el-input type="textarea" v-model="article.desc"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" native-type="submit">修改</el-button>
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
    saveArticle() {
      this.$http
        .put(`articles/${this.$route.params.id}`, this.article)
        .then((res) => {
          this.$message({
            message: "文章修改成功",
            type: "success",
          });
          this.$router.push("/articles/index");
        });
    },

    fetch() {
      this.$http.get(`articles/${this.$route.params.id}`).then((res) => {
        this.article = res.data;
      });
    },
  },
  created() {
    this.fetch();
  },
};
</script>
