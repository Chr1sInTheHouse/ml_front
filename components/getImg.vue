<template>
  <div class="con">
    <el-upload
      ref="upload"
      action="https://jsonplaceholder.typicode.com/posts/"
      list-type="picture-card"
      :auto-upload="false"
      :limit="1"
      :on-change="clog"
    >
      <el-button slot="trigger" size="small" type="info">select file</el-button>
      <el-button 
        style="margin-left: 10px"
        size="small"
        type="success"
        @click="submitUpload"
        >Upload</el-button
      >
    </el-upload>
    <img :src="url" class="upload-img" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      rater: "",
      image: "",
      limit_num: 1,
      url: "",
    };
  },
  methods: {
    async getImg() {
      img = await this.$axios.$get(
        "https://subjective-cp.herokuapp.com/request_image/name/" + this.rater
      );
      this.image = img.image;
    },
    submitUpload() {
      this.$refs.upload.submit();
    },
    clog(file) {
      console.log(file);
      this.url = file.url;
    },
  },
};
</script>

<style scoped>
.con {
  margin: 20px auto;
}

.upload-img {
  padding: 2%;
  max-height: 40%;
}
</style>