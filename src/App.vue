<template>
  <div>
    <div class="wrap">
      <div class="play_wrap" id="player">
        <div class="search_bar">
          <img src="./assets/images/player_title.png" alt />
          <input type="text" v-model="inpValue" @keyup.enter="search" />
        </div>
        <div class="center_con">
          <song-wrapper :songList="songList" @sind="getData" ref="song"></song-wrapper>
          <play-con :picUrl="picUrl" :flag="flag"></play-con>
          <comment-list :comments="comments" ref="hah"></comment-list>
        </div>
        <div>
          <audio-con :songUrl="songUrl" @bian="getFlag"></audio-con>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import songWrapper from "./components/songWrapper";
import playCon from "./components/playCon";
import commentList from "./components/commentList";
import audioCon from "./components/audioCon";
import axios from "axios";
export default {
  components: {
    songWrapper,
    playCon,
    commentList,
    audioCon
  },
  data() {
    return {
      inpValue: "",
      songList: [],
      songUrl: "",
      comments: [],
      picUrl: "",
      flag:false
    };
  },
  methods: {
    search: function() {
      axios({
        //因为有axious访问重复的地址会有缓存
        url:
          "http://183.237.67.218:3000/search?keywords=" +
          this.inpValue +
          "&&xxx=" +
          Math.random() * 99999
      }).then(res => {
        this.songList = res.data.result.songs;
        this.$refs.song.f5();
      });
    },
    getData: function(obj) {
      this.songUrl = obj.songUrl;
      this.comments = obj.comments;
      this.picUrl = obj.picUrl;
      this.$refs.hah.f5()
    },
    getFlag:function(flag){
      this.flag=flag
    }
  }
};
</script>

<style>
body,
ul,
dl,
dd {
  margin: 0px;
  padding: 0px;
}

.wrap {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: url("./assets/images/bg.jpg") no-repeat;
  background-size: 100% 100%;
}

.play_wrap {
  width: 800px;
  height: 544px;
  position: fixed;
  left: 50%;
  top: 50%;
  margin-left: -400px;
  margin-top: -272px;
  /* background-color: #f9f9f9; */
}

.search_bar {
  height: 60px;
  background-color: #1eacda;
  overflow: hidden;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
  z-index: 11;
}

.search_bar img {
  margin-left: 23px;
}

.search_bar input {
  margin-right: 23px;
  width: 296px;
  height: 34px;
  border-radius: 17px;
  border: 0px;
  background: url("./assets/images/zoom.png") 265px center no-repeat
    rgba(255, 255, 255, 0.45);
  text-indent: 15px;
  outline: none;
}

.center_con {
  height: 435px;
  background-color: rgba(255, 255, 255, 0.5);
  display: flex;
}

.song_wrapper {
  width: 200px;
  height: 435px;
  box-sizing: border-box;
  padding: 10px;
  list-style: none;
  background: url("./assets/images/line.png") right center no-repeat;
  position: relative;
  overflow: hidden;
}

.song_list li {
  font-size: 12px;
  color: #333;
  line-height: 36px;
  width: 180px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  cursor: pointer;
}

.song_list .active {
  color: #da651e;
}

.player_con {
  width: 400px;
  height: 435px;
  position: relative;
}

.disc {
  position: absolute;
  left: 73px;
  top: 60px;
  z-index: 9;
}

.cover {
  position: absolute;
  left: 125px;
  top: 112px;
  width: 150px;
  height: 150px;
  border-radius: 75px;
  z-index: 8;
}

.comment_list {
  width: 200px;
  height: 435px;
  box-sizing: border-box;
  padding: 10px;
  list-style: none;
  background: url("./assets/images/line.png") left center no-repeat;
  overflow: hidden;
  position: relative;
}

.comment_list dl {
  padding-left: 55px;
  position: relative;
  margin-bottom: 20px;
}

.comment_list dt {
  position: absolute;
  left: 4px;
  top: 0px;
}

.comment_list dt img {
  width: 40px;
  height: 40px;
  border-radius: 20px;
}

.comment_list dd {
  font-size: 12px;
}

.comment_list .name {
  font-weight: bold;
  color: #333;
  margin-top: 5px;
}

.comment_list .detail {
  color: #666;
  margin-top: 5px;
  line-height: 18px;
}

.audio_con {
  height: 50px;
  background-color: #f1f3f4;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}

.myaudio {
  width: 800px;
  height: 40px;
  margin-top: 5px;
  outline: none;
  background-color: #f1f3f4;
}

/* 旋转的动画 */
@keyframes Rotate {
  from {
    transform: rotateZ(0);
  }

  to {
    transform: rotateZ(360deg);
  }
}

/* 旋转的类名 */
.autoRotate {
  animation-name: Rotate;
  animation-iteration-count: infinite;
  animation-play-state: paused;
  animation-timing-function: linear;
  animation-duration: 5s;
}

/* 是否正在播放 */
.playing {
  animation-play-state: running;
}

.play_bar {
  position: absolute;
  left: 200px;
  top: -10px;
  z-index: 10;
  transform: rotate(-25deg);
  transform-origin: 12px 12px;
  transition: 1s;
}

/* 播放杆 转回去 */
.play_bar.playing {
  transform: rotate(0);
}
</style>
