<template>
  <div>
    <swiper ref="mySwiper" :options="swiperOptions" >
    <swiper-slide class="swiper-slide" v-for="item  in banners" :key="item.subCode">
      <a :href="item.link" >
        <img :src="item.image" alt="" >
      </a>
    </swiper-slide>
    <div class="swiper-pagination" slot="pagination"></div>
  </swiper>
  </div>
  
</template>


<script>
import {Swiper, SwiperItem, directive} from 'vue-awesome-swiper'

export default {
  name: 'HomeSwiper',
  props: {
    banners: {
      type: Array,
      default() {
        return []
      }
    }
  },
  components :{
    Swiper, SwiperItem, directive
  },
  data() {
      return {
        swiperOptions: {
          pagination: {
            el: '.swiper-pagination',
          },
          // Some Swiper option/callback...
          slidesPerView: 1,
          spaceBetween: 0,
          // centeredSlides: false,
          speed: 1000,
          onSlideChangeEnd: swiper => {
            //这个位置放swiper的回调方法
            this.page = swiper.realIndex+1;
            this.index = swiper.realIndex;
          },
          navigation: {
            nextEl: '.swiper-button-next',
            prevEl: '.swiper-button-prev',
          },
          //自动播放
          autoplay:{
            delay:2000,
            disableOnInteraction:false
          },
          pagination: {
            el: '.swiper-pagination',
            clickable: true,
          },
          //循环
          loop:true
        }
      }
    },
    computed: {
      swiper() {
        return this.$refs.mySwiper.$swiper
      }
    },
    mounted() {
      console.log('Current Swiper instance object', this.swiper)
      this.swiper.slideTo(0, 0, false)
    }
}
</script>
<style scoped>
  img {
    /* height: 180px;  */
    /* background-size: contain;  */
    height: 170px;
    width: 375px;
  }
  /* div .swiper-container {
    height: 100%;
    width: 100%;
    background-size: contain; 
  } */

</style>