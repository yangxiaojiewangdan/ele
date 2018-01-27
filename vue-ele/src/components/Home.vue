<template>
  <div class="hello">
      <div class="home-search">
        <div class="map">
          <i class="iconfont">&#xe60d;  </i>
          <span>东城区北京市政府</span>
          <i class="iconfont">&#xe600;</i>
        </div>
        <div class="search">
            <a href="/">
              <i class="iconfont">&#xe618;</i>
              <span>搜索商家、商品名称</span>
            </a>
        </div>
      </div>
      <mt-swipe class="swipe" :auto="4000">
            <mt-swipe-item>1</mt-swipe-item>
            <mt-swipe-item>2</mt-swipe-item>
            <mt-swipe-item>3</mt-swipe-item>
      </mt-swipe>
      <div class="home-img">
        <img src="https://fuss10.elemecdn.com/3/c8/45b2ec2855ed55d90c45bf9b07abbpng.png?imageMogr/format/webp/thumbnail/!710x178r/gravity/Center/crop/710x178/" alt="">
      </div>
      <div id="container">
      <mt-loadmore :top-method="loadTop" :bottom-method="loadBottom" :bottom-all-loaded="allLoaded" ref="loadmore">
          <ol>
            <dl v-for="item in 30" :key="item.id">{{ item }}</dl>
          </ol>
        </mt-loadmore>
</div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      list: [
        "https://pic.maizuo.com/usr/movie/1dd5e7d5618edcb603b67b7d85efbe71.jpg",
        "https://pic.maizuo.com/usr/movie/6f8d3193bc19f9a36e61abacd15b863a.jpg",
        "https://pic.maizuo.com/usr/movie/e044adec3a400f36c852b4b8061781f4.jpg",
        "https://pic.maizuo.com/usr/movie/d44e5dfcb60df8ac39c101b21cd8bf9d.jpg",
        "https://pic.maizuo.com/usr/movie/961391f7479f426b6584691330b2257f.jpg",
        "https://pic.maizuo.com/usr/movie/fc952ee11cf01366704dba86d94040f9.jpg",
        "https://pic.maizuo.com/usr/movie/76b217868630ec80a256f091a3619226.jpg"
      ],
      allLoaded: false
    }
  },
   methods: {
    loadTop() {
      console.log("loadTop");
      setTimeout(() => {
        Toast('数据重新加载完成');
        this.$refs.loadmore.onTopLoaded();
      }, 3000)
    },
    loadBottom() {
      
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

html,body{
  background-image: linear-gradient(90deg,#0af,#0085ff);
}
.hello{
  height: 100%;
}

/* header-nav */
.home-search{
  background-image: linear-gradient(90deg,#0af,#0085ff);
  color: #fff;
}

/* map */
.map{
  font-size: .18rem;
  height: .3.5rem;
  padding: 0.15rem .08rem 0;
}

/* search */
.search{
  position: sticky;
  top: 0px;
  z-index: 999;
  height: .5rem;
  font-size: 14px;
  background-image: linear-gradient(90deg,#0af,#0085ff);
}
.search>a{
  display: block;
  display: flex;
  width: 92%;
  height: .36rem;
  background-color: #fff;
  margin: .1rem auto 0.1rem;
  align-items: center;
  justify-content: center;
  color: #999;
  border-radius: .02rem;
}

/* swipe */
.swipe{
  height:2rem;
}

.home-img>img{
  width: 100%;
}
</style>
