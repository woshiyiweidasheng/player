<template>
  <div>
    <div class="song_wrapper" ref="scroll">
      <ul class="song_list">
        <li v-for="(item,i) in songList" :key="i" @dblclick="getAll(item.id)">{{item.name+" "+item.artists[0].name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import IScroll from "iscroll";
export default {
  props: ["songList"],
  data() {
    return {
      songUrl: "",
      comments: [],
      picUrl: "",
      myScroll: ""
    };
  },
  methods: {
    getAll: function(id) {
      //获取歌曲的地址
      axios({
        url: "http://183.237.67.218:3000/song/url?id=" + id
      })
        .then(res => {
          this.songUrl = res.data.data[0].url;
        })
        .catch(err => {
          console.log(err);
        });
      //获取歌曲的评论
      axios({
        url: "http://183.237.67.218:3000/comment/music?id=" + id
      })
        .then(res => {
          this.comments = res.data.hotComments;
        })
        .catch(err => {
          console.log(err);
        });
      //获取歌曲的详细信息
      axios({
        url: "http://183.237.67.218:3000/song/detail?ids=" + id
      })
        .then(res => {
          this.picUrl = res.data.songs[0].al.picUrl;
          this.$emit("sind", {
            songUrl: this.songUrl,
            comments: this.comments,
            picUrl: this.picUrl
          });
        })
        .catch(err => {
          console.log(err);
        });
    },
    f5:function(){
      this.$nextTick(()=>{
        this.myScroll.refresh();
      })
    }
  },
  mounted: function() {
    this.myScroll = new IScroll(this.$refs.scroll, {
      mouseWheel: true,
      scrollbars: true
    });
  }
};
</script>

<style>
</style>