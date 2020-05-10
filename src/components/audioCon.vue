<template>
  <div>
       <div class="audio_con">
          <audio @play="playEvent" @pause="pauseEvent" :src="songUrl" controls autoplay loop class="myaudio"></audio>
        </div>
  </div>
</template>

<script>
export default {
  props:['songUrl'],
  data() {
    return {
      flag:false
    }
  },
  methods:{
    playEvent:function(){
      this.flag=true;
      this.$emit('bian',this.flag)
    },
    pauseEvent:function(){
      this.flag=false;
      this.$emit('bian',this.flag)
    },
  }
}
</script>

<style>

</style>