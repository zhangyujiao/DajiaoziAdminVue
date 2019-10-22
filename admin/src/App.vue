<template>
  <div id="app">


      <div class="homepage-hero-module">
        <div class="video-container">
          <div :style="fixStyle" class="filter"></div>
          <video :style="fixStyle" autoplay loop class="fillWidth" v-on:canplay="canplay">
            <source src="./assets/logo.mp4" type="video/mp4"/>
          </video>
          <div class="poster hidden" v-if="!vedioCanPlay">
            <img :style="fixStyle" src="./assets/logo.jpg" alt="">
          </div>
        </div>
      </div>

    <el-row type="flex" justify="center">
      <el-form ref="loginForm" :model="user" status-icon label-width="80px">
        <el-form-item label="用户名" prop="name"></el-form-item>
      </el-form>
    </el-row>

    <!--<div class="note" :style ="note"></div>-->
    <!--<img src="./assets/logo.png">-->
    <h1>{{ msg }}</h1>
    <!--<HelloWorld/>-->
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      msg: 'hello word!',
      vedioCanPlay: false,
      fixStyle: ''
    }
    //username的校验规则
    const validateUsername = (rule, value, callback) => {
      // rule 对应的为loginRules.username的值
      if (!isvalidUsername(value)) {
        callback(new Error('请输入正确的用户名'))
      } else {
        callback()
      }
    }
    // password的校验规则
    const validatePass = (rule, value, callback) => {
      if (value.length < 5) {
        callback(new Error('密码不能小于5位'))
      } else {
        callback()
      }
    }
    return {
      // 表单校验规则
      loginRules: {
        //required 是否必须 trigger 触发条件 validator 该字段的校验规则
        username: [{required: true, trigger: 'blur', validator: validateUsername}],
        password: [{required: true, trigger: 'blur', validator: validatePass}]
      },
      // 表单提交对象
//      loginForm: {
//        username:
//      }
    }
  },
  methods: {
    canplay() {
      this.vedioCanPlay = true
    }
  },
  mounted: function() {
    window.onresize = () => {
      const windowWidth = document.body.clientWidth
      const windowHeight = document.body.clientHeight
      const windowAspectRatio = windowHeight / windowWidth
      let videoWidth
      let videoHeight
      if (windowAspectRatio < 0.5625) {
        videoWidth = windowWidth
        videoHeight = videoWidth * 0.5625
        this.fixStyle = {
          height: windowWidth * 0.6625 + 'px',
          width: windowWidth + 'px',
          'margin-bottom': (windowHeight - videoHeight)/2  + 'px',
          'margin-left': 'initial'
        }
      } else {
        videoHeight = windowHeight
        videoWidth = videoHeight / 0.5625
        this.fixStyle = {
          height: windowHeight + 'px',
          width: windowHeight / 0.5625 + 'px',
          'margin-left': (windowWidth - videoWidth) /2 + 'px',
          'margin-bottom': 'initial'
        }
      }
    }
    window.onresize()
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}
h1, h2 {
  font-weight: normal;
}


/*.homepage-hero-module,*/
.video-container {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.video-container .poster img,
.video-container video {
  z-index: 0;
  /*position: absolute;*/
}

.video-container .filter {
  z-index: 1;
  position: absolute;
  background: rgba(0, 0, 0, 0.1);
}
</style>
