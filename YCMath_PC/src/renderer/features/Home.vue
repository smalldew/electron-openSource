<template>
<el-container>
  <el-header>
    视频列表
  </el-header>
  <el-main>
      <div class="videoList" v-for="(item, index) in videoList" :key="index" @click="clickVideo(item.videoId)">
          <img :src="item.thumbnail"/>
          <p>{{item.name}}</p>
      </div>
  </el-main>
</el-container>
</template>



<script>
import axios from "axios"

export default {
   name: 'home',
   data() {
       return {
           videoList: [],
           msg: '这里是首页'
       }
   },
   methods: {
       getVideoList(){
            let that = this
            axios({
                method: 'get',
                url: 'https://api-wx-test.yangcong345.com/parents/course/homepage'
            }).then(res => {
                if(res.data.noPay.videos) {
                   this.videoList = res.data.pay.videos
                }
            }) 
       },
       clickVideo(videoId) {
           this.$router.push({path:'/video', query:{videoId: videoId}})
       }
   },
   mounted() {
       this.getVideoList()
   }   
}
</script>



<style scoped>
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
    text-align: center;
  }
  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    line-height: 160px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .videoList {
    width: 400px;
    height: 320px;
    margin-top: 20px;
    background: white;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .videoList img {
    width: 340px;
    height: 180px;
  }
  .videoList p {
    width: 100%;
    height: 80px;
    line-height: 80px;
    text-align: center;
  }

</style>

