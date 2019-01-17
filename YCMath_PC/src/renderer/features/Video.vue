<template>
<el-container>
  <el-header>
    <el-button class="backButton" @click="backHome">返回</el-button>
  </el-header>
  <el-main>
    <video :src="videoSrc" controls="controls"></video>
  </el-main>
</el-container>
</template>


<script>
import axios from "axios"


export default {
    data() {
        return {
           videoId: '',
           videoSrc: ''
        }
    },
    methods: {
        // 获取参数
        getQuery() {
            let that = this
            that.videoId = that.$route.query.videoId
        },   
        getVideo() {
            let that = this
            axios({
                method: 'get',
                url: `https://api-wx-test.yangcong345.com/parents/course/videoUrl?id=${that.videoId}`
            }).then(res => {
                if(res.data.ok) {
                   that.videoSrc = res.data.url
                }
            }) 
        },
        backHome() {
          this.$router.push('/')
        },
    },
    mounted() {
        let that = this
        that.getQuery()
        that.getVideo()
    }
}
</script>

<style scoped>
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    line-height: 60px;
  }
  .el-header p {
    background-color: #B3C0D1;
    color: red;
    line-height: 60px;
  }
  .backButton {
    margin-left: 0px;
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
</style>
