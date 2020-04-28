<template>
  <div>
    <div id="top-image">
      <img src="../assets/top-image.png" />
    </div>
    <div id="title-area">
      <span class="test-title emphasis">식탐&nbsp;</span>
      <span class="test-title">테스트</span>
    </div>
    <div class="sub-title-area">
      <span class="test-sub-title">쉬우니깐 한번 해보세요.🤫</span>
    </div>
    <div
      id="test-window"
      v-bind:class="[windowColor, windowBackground, windowOpacity, size]"
      @click="click()"
    >
      <div>
        <div
          class="result-message"
          v-if="this.totalTime != '' && !this.canRetry"
        >{{totalTime}}ms, {{round}}/{{totalRound}}</div>
        <div class="click-message" v-if="!this.isStart && this.round == 0">시작하려면 클릭</div>
        <div class="click-message" v-if="!this.isStart && this.round != 0 && !this.canRetry">다시 시작하려면 클릭</div>
      </div>
      <div class="test-message" v-if="this.isWait">먹을 게 나오면 재빠르게 터치!</div>
      <div v-if="this.canRetry">
        <div class="click-message">평균 {{mean}}ms</div>
        <div class="click-message">오이도 음식이다.</div>
        <a class="myButton" @click="retry()">다시 시작하기</a>
      </div>
    </div>
    <div>공유하기</div>
  </div>
</template>

<script>
// import Typer from '../components/Typer.vue';
export default {
  props: {
    msg: String
  },
  components: {
    // Typer
  },
  data() {
    return {
      startTime: "",
      endTime: "",
      totalTime: "",
      isStart: false,
      windowColor: "before",
      windowBackground: "",
      round: 0,
      totalRound: 5,
      isWait: false,
      windowOpacity: "",
      size: "",
      windowWidth: 0,
      results: [],
      canRetry: false
    };
  },
  methods: {
    startTest: function() {
      this.windowOpacity = "";
      this.round = this.round + 1;
      this.isStart = true;
      this.isWait = true;
      this.changeColor("before");
      this.totalTime = "";
      const vm = this;
      const waitTime = 2000 + Math.random() * 5000;
      setTimeout(() => vm.changeBackground(), waitTime);
    },
    changeColor: function(color) {
      this.windowColor = color;
      this.windowBackground = "";
    },
    changeBackground: function() {
      this.startTime = new Date();
      this.isWait = false;
      this.windowBackground = "food-" + this.round;
    },
    click: function() {
      if (this.isWait) {
        alert("배고픕니까?");
        location.reload();
      } else {
        if (!this.isStart) {
          this.startTest();
        } else {
          this.endTest();
        }
      }
    },
    endTest: function() {
      this.windowOpacity = "windowOpacity";
      this.isStart = false;
      this.endTime = new Date();
      this.totalTime = this.endTime - this.startTime;
      this.results.push(this.totalTime);
      (this.startTime = ""), (this.endTime = "");
      if (this.round == 5) {
        this.showRetry();
      }
    },
    showRetry() {
      this.canRetry = true;
    },
    retry() {
      location.reload();
    },
    changeSize() {
      if (this.windowWidth > 700) {
        this.size = "desktop";
      } else {
        this.size = "";
      }
    }
  },
  created() {
    this.windowWidth = window.innerWidth;
    window.addEventListener("resize", function() {
      this.windowWidth = window.innerWidth;
    });
    // console.log(this.windowWidth)
    this.changeSize();
  },
  watch: {
    windowWidth() {
      this.changeSize();
    }
  },
  computed: {
    mean: function() {
      return this.results.reduce((prev, curr) => prev + curr) / this.results.length;
    }
  }
};
</script>

<style>
img {
  max-width: 60px;
  max-height: 10%;
}
/* #top-image {
  max-width:100%;
  max-height:100%;
} */
#title-area {
  margin-top: 17px;
}
.test-title {
  font-weight: bold;
  font-size: 45px;
}
.test-title.emphasis {
  color: brown;
  font-size: 50px;
}
.test-sub-title {
  font-size: 25px;
}
.sub-title-area {
  margin-bottom: 10px;
}
.before {
  background-color: #d7bde2;
}
.after {
  background-color: steelblue;
}
.click-message {
  font-size: 35px;
  color: white;
}
#test-window {
  width: 100%;
  height: 240px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  background-position: center center;
  background-repeat: no-repeat;
}
#test-window.desktop {
  height: 500px;
}
#test-window.food-1 {
  background-image: url("https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2Fcx4HCH%2FbtqDMGXsdbK%2FAvHfC1qomNDONaq45adDQ1%2Fimg.jpg");
  background-size: 100%;
  background-position: center center;
}
#test-window.food-2 {
  background-image: url("https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FEDnmK%2FbtqDNooDLPw%2FKkEebnFtYKqtV71UlF39Qk%2Fimg.jpg");
  background-size: 100%;
  background-position: center 83%;
}
#test-window.food-3 {
  background-image: url("https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2F73PTN%2FbtqDMj9cOVZ%2FnaDHTT1VKJe6KBAdMXtUEk%2Fimg.jpg");
  background-size: 100%;
  background-position: center center;
}
#test-window.food-4 {
  background-image: url("https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2F1C5BI%2FbtqDMi3t46k%2FJnUM0lOkvPMMeKbqsOdcYK%2Fimg.jpg");
  background-size: 100%;
  background-position: center center;
}
#test-window.food-5 {
  background-image: url("https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2F6OZqS%2FbtqDMktslQp%2FSsUtMaBMqHHu8hJr6ttomk%2Fimg.jpg");
  background-size: 100%;
  background-position: center center;
}
#test-window.windowOpacity {
  opacity: 0.6;
}
.test-message {
  font-size: 25px;
  color: white;
}
.result-message {
  font-size: 25px;
  color: white;
}
.myButton {
  background-color: #44c767;
  border-radius: 11px;
  border: 3px solid #18ab29;
  display: inline-block;
  cursor: pointer;
  color: #ffffff;
  font-family: Arial;
  font-size: 21px;
  padding: 16px 37px;
  text-decoration: none;
  text-shadow: 0px 0px 0px #2f6627;
}
.myButton:hover {
  background-color: #d7bde2;
}
.myButton:active {
  position: relative;
  top: 1px;
}
</style>
