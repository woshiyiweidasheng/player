<template>
  <div>
    <div class="comment_list" ref="scroll">
      <div>
        <dl v-for="(item,i) in comments" :key="i">
          <dt>
            <img :src="item.user.avatarUrl" alt />
          </dt>
          <dd class="name">{{item.user.nickname}}</dd>
          <dd class="detail">{{item.content}}</dd>
        </dl>
      </div>
    </div>
  </div>
</template>

<script>
import IScroll from "iscroll";
export default {
  props: ["comments"],
  data() {
    return {
      myScroll: ""
    };
  },
  methods: {
    f5: function() {
      this.$nextTick(() => {
        this.myScroll.refresh();
      });
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