<template>
  <div class="my-carousel" :style="'height:'+height+'px;'" ref="myCarousel">
    <div v-if="show">
      <div v-for="(item,index) in carouselListData" :key="index" class="my-carousel-item" :style="'transform: translateX('+(1 * parentWidth/(showSize || 1)) * index+'px);width:'+(100/(showSize || 1))+'%'">
        <img :src="item.url" alt="img" @click="window.open(item.link)">
      </div>
      <div class="arrow arrow-left" @click="next()">
        <i class="el-icon-arrow-right"></i>
      </div>
      <div class="arrow arrow-right" @click="last()">
        <i class="el-icon-arrow-left"></i>
      </div>
    </div>
  </div>

</template>

<script>
  export default {
    name: "my-carousel",
    props: ['carouselList', 'interval', 'height', 'autoplay','showSize'],
    data() {
      return {
        carouselListData: [],
        timmer: null,
        parentWidth:'100%',
        show:false
      }
    },
    created() {
      this.carouselListData = JSON.parse(JSON.stringify(this.carouselList))
      if (this.autoplay && this.carouselListData.length > 0) {
        this.timmer = setInterval(() => {
          this.next()
        }, this.interval || 5000)
      }

    },
    mounted(){
      this.parentWidth = this.$refs.myCarousel.clientWidth
      this.show = true
    },
    beforeDestroy() {
      if (this.timmer) {
        clearInterval(this.this.timmer)
      }
    },
    methods: {
      last() {
        let obj = this.carouselListData.slice(0, 1);
        this.carouselListData.splice(0, 1);
        this.carouselListData.push(obj[0]);
      },
      next() {
        let obj = this.carouselListData.slice(this.carouselListData.length - 1, this.carouselListData.length);
        this.carouselListData.splice(this.carouselListData.length - 1, 1);
        this.carouselListData = obj.concat(this.carouselListData);
      },
    },

  }
</script>

<style scoped>
  .my-carousel {
    position: relative;
    width: 100%;
    overflow: hidden;
  }

  .my-carousel-item {
    background: #ccc;
    position: absolute;
    height: 100%;
    overflow: hidden;
    transition: transform 3s linear;
  }

  img {
    width: 100%;
  }

  .arrow {
    color: #fff;
    position: absolute;
    z-index: 999;
    top: 50%;
    margin-top: -20px;
  }

  i {
    height: 40px;
    width: 40px;
    border-radius: 100%;
    background: rgba(0, 0, 0, .1);
    line-height: 40px;
    box-sizing: border-box;
  }

  .arrow.arrow-left {
    left: 0;
    margin-left: -20px;
    text-align: right;
  }

  i {
    padding-right: 6px
  }

  .arrow.arrow-right {
    right: 0;
    margin-right: -20px;
    text-align: left;
  }

  i {
    padding-left: 6px;
  }

</style>
