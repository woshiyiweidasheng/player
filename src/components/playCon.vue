<template>
  <div>
       <div class="player_con">
            <img src="../assets/images/player_bar.png" class="play_bar " :class="{'playing':flag}" />
            <!-- 黑胶碟片 -->
            <img src="../assets/images/disc.png" class="disc autoRotate " :class="{'playing':flag}"/>
            <img :src="picUrl" class="cover autoRotate " :class="{'playing':flag}"/>
          </div>
  </div>
</template>

<script>
export default {
  props:['picUrl','flag']
}
</script>

<style>

</style>