<template>
  <div class="all">
    <div id="top" class="container">
      <div class="con">
        <el-upload
          ref="upload"
          action="/predict"
          list-type="picture-card"
          :auto-upload="false"
          :limit="1"
          :on-change="clog"
        >
          <el-button slot="trigger" size="small" type="info"
            >select file</el-button
          >
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
      <el-button
        class="scroll"
        v-scroll-to="'#score'"
        icon="el-icon-arrow-down"
        size="large"
      />
    </div>
    <div id="score" class="container">
      <p
        class="data"
        data-aos="fade-up"
        data-aos-anchor="#top"
        data-aos-delay="300"
        data-aos-anchor-placement="center-top"
      >
        hit point: {{ power[0] }}
      </p>
      <p
        class="data"
        data-aos="fade-up"
        data-aos-anchor="#top"
        data-aos-delay="500"
        data-aos-anchor-placement="center-top"
      >
        physic attack: {{ power[1] }}
      </p>
      <p
        class="data"
        data-aos="fade-up"
        data-aos-anchor="#top"
        data-aos-delay="700"
        data-aos-anchor-placement="center-top"
      >
        magic attack: {{ power[2] }}
      </p>
      <p
        class="data"
        data-aos="fade-up"
        data-aos-anchor="#top"
        data-aos-delay="900"
        data-aos-anchor-placement="center-top"
      >
        speed: {{ power[3] }}
      </p>
      <p
        class="data"
        data-aos="fade-up"
        data-aos-anchor="#top"
        data-aos-delay="1100"
        data-aos-anchor-placement="center-top"
      >
        crit: {{ power[4] }}
      </p>
      <p
        class="job"
        data-aos="flip-left"
        data-aos-anchor="#top"
        data-aos-delay="1500"
        data-aos-anchor-placement="center-top"
      >
        你是一位 {{ level[level_idx] }} {{ job[job_idx] }}
      </p>
    </div>
  </div>
</template>

<script>

export default {
  data() {
    return {
      power: [1, 2, 3, 4, 5],
      level_idx: 2,
      job_idx: 4,
      level: ["見習", "專業", "鑽石", "宗師", "傳說"],
      job: ["坦克", "戰士", "法師", "刺客", "暴徒"],
      url: "",
    };
  },
  methods: {
    async getResult() {
      this.image = img.image;
    },
    submitUpload() {
      result = this.$refs.upload.submit();
      this.power[0] = result["hp"];
      this.power[1] = result["pa"];
      this.power[2] = result["ma"];
      this.power[3] = result["sp"];
      this.power[4] = result["cr"];
      let best = 0;
      for(let i=0; i<5; i++){
        if(power[i]>best){
          best = power[i];
          this.job_idx = i;
          this.level_idx = Math.floor(best/2);
        }
      }
    },
    clog(file) {
      console.log(file);

      this.url = file.url;
    },
  },
};
</script>

<style>
.all {
  background-image: url("/wee_dark.png");
  background-size: 100% auto;
  background-position: center center;
  background-repeat: repeat-y;
}

.container {
  margin: 0 auto;
  max-width: 100%;
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  min-height: 100vh;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}

.con {
  margin: 20px auto;
}

.upload-img {
  padding: 2%;
  max-height: 40%;
}

.scroll {
  font-size: 80px;
  width: 100%;
  background: transparent;
  border: 0px;
  padding: 0;
  position: fixed;
  bottom: 0%;
  left: 0;
}

.scroll:hover {
  font-size: 80px;
  width: 100%;
  background: transparent;
  border: 0px;
  padding: 0;
  position: fixed;
  bottom: 0%;
  left: 0;
}

.scroll:focus {
  font-size: 80px;
  width: 100%;
  background: transparent;
  border: 0px;
  padding: 0;
  position: fixed;
  bottom: 0%;
  left: 0;
}

.data {
  padding-top: 3%;
  font-size: 40px;
  font-family: "Courier New", Courier, monospace;
  color: white;
  text-align: center;
}

.job {
  padding-top: 3%;
  font-size: 40px;
  font-family: "Courier New", Courier, monospace;
  color: white;
  text-align: center;
}

#score {
  display: block;
}
</style>
