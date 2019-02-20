<template>
  <div class="swiper-container mz-banner">
    <div class="swiper-wrapper">
      <div class="swiper-slide"
      v-for="item in bannerList"
      :key="item._id">
      <img :src="item.imgUrl" alt="">
      </div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>
  </div>
</template>

<script>
// 使用axios调用后台的接口

// 1.引入
import axios from 'axios';

// 2. 调用 axios.get（'http://localhost:3000/banner/search'）
export default {
  data () {
    return {
      // 轮播图的数据
      bannerList: []
    }
  },
  created () {
    var that = this;
    axios.get('http://localhost:3000/banner/search?pageSize=10').then(function (res) {
      console.log(res);
      let data = res.data;
      that.bannerList = data.data;

      setTimeout(() => {
      /* eslint-disable */
      new Swiper(".swiper-container", {
      autoplay: true,
      loop: true, // 循环模式选项
      // 如果需要分页器
      pagination: {
      el: ".swiper-pagination"
      }
      });
    /* eslint-enable */
      }, 1000)
    });
  },

  mounted () {
    // 对某个代码不校验 eslint 的规则
  }
};
</script>

<style lang="less">
.mz-banner {
  img{
    width: 100%;
  }
  height: 210px;
}

.swiper-pagination-bullet {
  width: 8px!important;
  height: 8px!important;
  border: 2px solid #ffffff!important;
  opacity: .5;
}
</style>
