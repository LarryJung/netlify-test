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
      v-bind:class="[windowColor, windowBackground, windowOpacity, size, clickable]"
      @click="click()"
    >
      <div>
        <div
          class="result-message"
          v-if="this.totalTime != '' && !this.canRetry"
        >{{totalTime}}ms, {{round}}/{{totalRound}}</div>
        <div class="click-message" v-if="!this.isStart && this.round == 0">시작하려면 클릭</div>
        <div
          class="click-message"
          v-if="!this.isStart && this.round != 0 && !this.canRetry"
        >다시 시작하려면 클릭</div>
      </div>
      <div class="test-message" v-if="this.isWait">먹을 게 나오면 재빠르게 터치!</div>
      <div v-if="this.canRetry">
        <div>
          <span class="click-message">평균 {{mean}}ms</span>
          <span style="color: white;">({{getLevel()}})</span>
        </div>
        <div class="click-message" @click="retry()">
          오이도 음식이다.
          <span>
            <svg
              class="bi bi-arrow-counterclockwise retry-icon"
              width="1em"
              height="1em"
              viewBox="0 0 16 16"
              fill="currentColor"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                fill-rule="evenodd"
                d="M12.83 6.706a5 5 0 00-7.103-3.16.5.5 0 11-.454-.892A6 6 0 112.545 5.5a.5.5 0 11.91.417 5 5 0 109.375.789z"
                clip-rule="evenodd"
              />
              <path
                fill-rule="evenodd"
                d="M7.854.146a.5.5 0 00-.708 0l-2.5 2.5a.5.5 0 000 .708l2.5 2.5a.5.5 0 10.708-.708L5.707 3 7.854.854a.5.5 0 000-.708z"
                clip-rule="evenodd"
              />
            </svg>
          </span>
        </div>
        <div style="margin-top: 30px">
          <span>
            <div v-if="this.canRetry">
              <div class="share-button">
                <div class="share-button__back">
                  <a class="share__link" href="#" title="kakaotalk" @click="sendKakao()">
                    <svg
                      class="share__icon share__icon--kakaotalk"
                      xmlns="http://www.w3.org/2000/svg"
                      xmlns:xlink="http://www.w3.org/1999/xlink"
                      width="1.08em"
                      height="1em"
                      style="-ms-transform: rotate(360deg); -webkit-transform: rotate(360deg); transform: rotate(360deg);"
                      preserveAspectRatio="xMidYMid meet"
                      viewBox="0 0 1792 1664"
                    >
                      <path
                        d="M896 12q243 0 449.5 94.5t326.5 257T1792 718t-120 355t-326 257.5t-450 94.5q-77 0-159-11q-356 247-379 250q-11 4-21-1q-4-3-6-8t-2-9v-4q6-39 91-325q-193-96-306.5-254.5T0 718q0-192 120-354.5t326.5-257T896 12zM442 905V598h79q16 0 33.5-11.5T572 555t-16-33.5t-31-13.5H265q-17 0-32 10t-15 33t16 35t36 12h79v307q0 25 12 41t34 16t34.5-18t12.5-39zm433 57q37-14 23-71q-4-13-56.5-155.5T781 573q-27-65-74-65q-51 0-79 65q-8 17-61 165.5T512 891q-7 9-3.5 33t21.5 33q20 9 39 2t26-21l24-66h174q11 36 16 47q5 10 11 20t22 19.5t33 3.5zm269 0q21 0 38.5-13t17.5-35t-16-34.5t-40-12.5h-111V565q0-21-12.5-39T986 508t-34 16t-12 41v340q0 25 12 41t34 16q1 0 3.5-.5t3.5-.5t3.5.5t3.5.5h144zm394-7q17-16 17-36.5t-13-36.5q-6-9-126-169q58-59 117-118q15-15 18.5-35.5T1540 521q-17-16-36.5-13t-36.5 20q-3 3-26 26.5t-59.5 60.5t-64.5 66V565q0-21-12.5-39t-34.5-18t-34 16t-12 41v340q0 25 12 41t34 16t34.5-18t12.5-39v-91q4-4 15-15.5t18-18.5q66 90 118 159q14 19 32.5 24.5t37.5-8.5zM646 782l61-179l60 179H646z"
                        fill="#FFFFFF"
                      />
                    </svg>
                  </a>
                  <a class="share__link" href="#" title="facebook" @click="sendFacebook()">
                    <svg
                      class="share__icon share__icon--facebook"
                      version="1.1"
                      xmlns="http://www.w3.org/2000/svg"
                      xmlns:xlink="http://www.w3.org/1999/xlink"
                      x="0px"
                      y="0px"
                      width="49.652px"
                      height="49.652px"
                      viewBox="0 0 49.652 49.652"
                      style="enable-background:new 0 0 49.652 49.652;"
                      xml:space="preserve"
                    >
                      <g>
                        <g>
                          <path
                            d="M24.826,0C11.137,0,0,11.137,0,24.826c0,13.688,11.137,24.826,24.826,24.826c13.688,0,24.826-11.138,24.826-24.826    C49.652,11.137,38.516,0,24.826,0z M31,25.7h-4.039c0,6.453,0,14.396,0,14.396h-5.985c0,0,0-7.866,0-14.396h-2.845v-5.088h2.845    v-3.291c0-2.357,1.12-6.04,6.04-6.04l4.435,0.017v4.939c0,0-2.695,0-3.219,0c-0.524,0-1.269,0.262-1.269,1.386v2.99h4.56L31,25.7z    "
                          />
                        </g>
                      </g>
                    </svg>
                  </a>
                  <a
                    class="share__link clipboard"
                    v-bind:data-clipboard-text="this.currentUrl"
                    href="#"
                    title="copy"
                  >
                    <svg
                      class="share__icon share__icon--copy"
                      xmlns="http://www.w3.org/2000/svg"
                      xmlns:xlink="http://www.w3.org/1999/xlink"
                      aria-hidden="true"
                      focusable="false"
                      width="1em"
                      height="1em"
                      style="-ms-transform: rotate(360deg); -webkit-transform: rotate(360deg); transform: rotate(360deg);"
                      preserveAspectRatio="xMidYMid meet"
                      viewBox="0 0 24 24"
                    >
                      <path
                        d="M19 21H8V7h11m0-2H8a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h11a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2m-3-4H4a2 2 0 0 0-2 2v14h2V3h12V1z"
                        fill="#FFFFFF"
                      />
                    </svg>
                  </a>
                </div>
                <div class="share-button__front">
                  <p class="share-button__text">별걸 다 공유하기</p>
                </div>
              </div>
            </div>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
var clipboard = new Clipboard(".clipboard");
clipboard.on("success", function(e) {
  alert("주소가 복사되었습니다.");
  console.log(e);
});
clipboard.on("error", function(e) {
  console.log(e);
});
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
      canRetry: false,
      clickable: "",
      currentUrl: window.location.href
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
      if (this.canRetry) {
        return;
      }
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
    },
    getLevel() {
      if (this.mean > 400) {
        return "상당히 배가 고프다.";
      }
      if (this.mean > 600) {
        return "적당히 배가 고프다.";
      }
      if (this.mean > 800) {
        return "그저 든든한 상태이다.";
      }
      if (this.mean > 1000) {
        return "그닥 땡기지 않는다.";
      }
      return "나는 배가 부르다.";
    },
    sendKakao() {
      Kakao.Link.sendDefault({
        objectType: "feed",
        content: {
          title: "식탐 테스트 결과",
          imageUrl: "",
          link: {
            webUrl: this.currentUrl,
            mobileWebUrl: this.currentUrl
          },
          description: this.getLevel()
        },
        buttons: [
          {
            title: "진단하러가기",
            link: {
              webUrl: this.currentUrl,
              mobileWebUrl: this.currentUrl
            }
          }
        ],
        success: function(response) {
          console.log("success");
          console.log(response);
        },
        fail: function(error) {
          console.log("error");
          console.log(error);
        }
      });
    },
    sendFacebook() {
      alert("준비중입니다.");
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
      return (
        this.results.reduce((prev, curr) => prev + curr) / this.results.length
      );
    }
  },
  mounted() {}
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
.retry-icon:hover {
  color: black;
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
  z-index: -1;
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
.result-message:hover {
  color: grey;
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

@import url("https://fonts.googleapis.com/css?family=Roboto:300i,400");

.share__icon {
  width: 40px;
  height: 40px;
  fill: #fff;
  display: inline-block;
  vertical-align: top;
  margin-right: 10px;
}
.share__icon:last-of-type {
  margin-right: 0px;
}

.share-button {
  cursor: pointer;
  display: inline-block;
  /* height: 42px; */
  /* position: absolute; */
  /* top: 50%; */
  /* transform: translateY(-50%) translateX(-50%);
  -webkit-transform: translateY(-50%) translateX(-50%);
  -moz-transform: translateY(-50%) translateX(-50%); */
  /* left: 50%; */
  -webkit-perspective: 200px;
  -moz-perspective: 200px;
  perspective: 200px;
}

.share-button__back {
  background-color: #368b8b;
  padding: 5px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0px 0px 14px rgba(0, 0, 0, 0.1) inset;
}

.share-button__front {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background-color: #fff;
  border-radius: 20px;
  position: absolute;
  top: 0;
  left: 0;
  transform-origin: center top;
  -webkit-transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  -moz-transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  -ms-transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  -o-transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  -webkit-transform-style: preserve-3d;
  -moz-transform-style: preserve-3d;
  -webkit-backface-visibility: hidden;
  -moz-backface-visibility: hidden;
}

.share-button__text {
  margin: 0;
  line-height: 42px;
  font-size: 16px;
  text-align: center;
  color: #b6b6b6;
}

.share__link {
  position: relative;
  top: 40px;
  display: inline-block;
  opacity: 0;
  -webkit-transition: top 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  -moz-transition: top 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  -ms-transition: top 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  -o-transition: top 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  transition: top 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  margin-left: 5px;
}

.share-button:hover .share-button__front {
  transform: rotateX(90deg);
}

.share-button:hover .share__link {
  top: 0;
  opacity: 1;
}

.share-button:hover .share__link:nth-of-type(1) {
  transition-delay: 0.1s;
}

.share-button:hover .share__link:nth-of-type(2) {
  transition-delay: 0.2s;
}

.share-button:hover .share__link:nth-of-type(3) {
  transition-delay: 0.3s;
}

.share-button:hover .share__link:nth-of-type(4) {
  transition-delay: 0.4s;
}
</style>
