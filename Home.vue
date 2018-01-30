<template>
  <div class="home">
      <div class="home-search">
        <div class="map">
          <i class="iconfont">&#xe60d;</i>
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
            <mt-swipe-item>
              <a href="#"  v-for="item in list" class="gooding" :key="item.id">
                <img :src="'http://fuss10.elemecdn.com/'+item.image_hash+'.jpeg?imageMogr/format/webp/thumbnail/!90x90r/gravity/Center/crop/90x90/'" alt="">
               <span>{{item.name}}</span>
               </a>
            </mt-swipe-item>
             <mt-swipe-item>
               <a href="#"  v-for="item in list2" class="gooding" :key="item.id">
                <img :src="'http://fuss10.elemecdn.com/'+item.image_hash+'.jpeg?imageMogr/format/webp/thumbnail/!90x90r/gravity/Center/crop/90x90/'" alt="">
                {{item.name}}</a>
             </mt-swipe-item>
      </mt-swipe>
      
      <div class="home-img">
        <img src="https://fuss10.elemecdn.com/3/c8/45b2ec2855ed55d90c45bf9b07abbpng.png?imageMogr/format/webp/thumbnail/!710x178r/gravity/Center/crop/710x178/">
      </div>
      <div id="container"></div>
      <div class="lb-tj">
            <h3>推荐商家</h3>
          </div>
      <mt-loadmore class="lb" :top-method="loadTop" :bottom-method="loadBottom" :bottom-all-loaded="allLoaded" ref="loadmore">
          <ol v-for="item in list3" :key="item.id">
            <dl class="dl1">
              <div class="home-box">
                <img :src="'https://fuss10.elemecdn.com/'+ item.restaurant.image_path+ '.'+ item.restaurant.image_path.split('').slice(32,).join('') +'?imageMogr/format/webp/thumbnail/!130x130r/gravity/Center/crop/130x130/'">
              </div>
              <div class="zl">
                <section>
                  <b class="b1">品牌</b>
                  <span class="span1">{{item.restaurant.name}}</span>
                </section>
                <section>
                  <span>*****</span>
                  <span>{{item.restaurant.rating}}</span>
                  <span>月销售1719单</span>
                  <span class="span2">{蜂鸟专送}</span>
                  
                </section>
                <section>
                  <span>￥{{item.restaurant.piecewise_agent_fee.rules[0].price}}起送</span>
                  <span>配送费{{item.restaurant.piecewise_agent_fee.description}}</span>
                  <span class="span3">{{parseInt(item.restaurant.distance/60)}}分钟</span>
                  <span class="span4">|</span>
                  <span class="span5">{{item.restaurant.distance/100}}km</span>
                </section>
              </div>
            </dl>
            <dl class="dl2">
                <section class="koubei">
                  <img src="https://fuss10.elemecdn.com/a/c1/24c767ffa7fd296d3e2d6f01798c6png.png?imageMogr/format/webp/thumbnail/!60x60r/gravity/Center/crop/60x60/">
                  <span class="span6">{{item.restaurant.recommend.reason}}</span>
                </section>
                <section class="xuxian"><em></em></section>
                <section class="huodong">
                  <div class="zhekou">
                    <div class="shou">
                      <span class="span7">首</span>
                      <span>新用户下单立减17元</span>
                      <i class="iconfont">&#xe600;</i>
                    </div>
                    <div class="jian">
                      <span class="span8">减</span>
                      <span>满28减17，满40减22，满60减30</span>
                    </div>
                  </div>
                  <div class="huo">
                    <span>10活动</span>
                    <i class="iconfont" style="font-size:10px;">&#xe600;</i>
                    <i></i>
                  </div>
                </section>
              </dl>
          </ol>

        </mt-loadmore>
    
  </div>
</template>

<script>
import axios from 'axios';
import { Toast } from 'mint-ui';
export default {
  name: 'Home',
  data () {
    return {
      list: [],
      list2:[],
      list3:[],
      allLoaded: false
    }
  },
  mounted() {
    console.log(this);
    console.log(this.$route.params.id);
    var id = this.$route.params.id;
    axios.get("/restapi/shopping/openapi/entries?latitude=39.90469&longitude=116.407173&templates[]=main_template&templates[]=favourable_template&templates[]=svip_template")
    .then((res)=>{
      console.log(res)
      this.list = res.data[0].entries
      this.list2 = this.list.slice(10,)
      this.list = this.list.slice(0,10)
    }),
    axios.get("/restapi/shopping/v3/restaurants?latitude=39.90469&longitude=116.407173&offset=0&limit=8&extras[]=activities&extras[]=tags&extra_filters=home&rank_id=&terminal=h5")
    .then((res)=>{
      console.log(res)
      this.list3=res.data.items
    })
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
<style>
.home{
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
  padding: 0.25rem .08rem 0;
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
  width: 100%;
  height:1.77rem;
}
.gooding{
  display: flex;
  width: 20%;
  height: 70px;
  font-size: 12px;
  float: left;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: .1rem;
  color: #999;
}
.gooding img{
  width: .45rem;
  height: .45rem;
}
.mint-swipe-indicators {
    position: absolute;
    bottom: -20px;
    left: 50%;
    -webkit-transform: translateX(-50%);
            transform: translateX(-50%);
}
/* img */
.home-img{
  height: .89rem;
  margin:0 .08rem;
  padding-bottom: .1rem;
}
.home-img>img{
  display: block;
  width: 100%;
}
#container{
  height: .1rem;
  background-color: #fff;
}

/* liebiao */
.lb{
  height: 100%;
  font-size: 14px;
}
.lb-tj{
  height: .36rem;
  text-align: center;
  line-height: .36rem;
  display: flex;
  flex-direction: column;
  position: relative;
}
h3{
  color: #666;
  font-size: .14rem;
}
h3:before{
    display: block;
    content: "";
    width: .2rem;
    height: .01rem;
    background-color: #999;
    position: absolute;
    top: .18rem;
    left: 63%;
    color: #999
}
h3:after{
    display: block;
    content: "";
    width: .2rem;
    height: .01rem;
    background-color: #999;
    position: absolute;
    top: .18rem;
    left: 30%;
    color: #999;
}

/* home-box */
ol{
  min-height: 1.55rem;
  margin: 0.1rem 0;
  border-top: 1px dotted #999;
}
ol dl{
  margin: 0 .08rem;
}
.dl1{
  display: flex;
  flex-direction: row;
}
.home-box{
  height: .65rem;
}
.home-box img{
  height: .65rem;
}
.zl{
  font-size: .10rem;
  margin-left:.1rem; 
  display: flex;
  flex:1;
  flex-direction: column;
  justify-content:space-around;
}
.b1{
  background-image: linear-gradient(-139deg,#fff100,#ffe339);
  padding: .02rem .03rem;
  border-radius: .04rem;
}
.span1{
  font-size: .14rem;
  font-weight: 600;
}
.span2{
  float:right;
  background-image:linear-gradient(45deg,#0085ff,#0af);
  color: #fff;
  border-radius: .04rem;
  font-size: .08rem;
}
.span3{
  float: right;
}
.span4{
  float:right;
  margin:0  0.04rem;
  color: #ddd;
}
.span5{
  float:right;
}
.dl2{
  padding-left:22%;
  font-size: .1rem;
  margin: 0;
}
.dl2>section>img{
  width: .1rem;
  height: .1rem;
}
.span6{
  font-size: 10px;
  color: rgb(232, 71, 11);
}
.span7{
  background-color: rgb(112, 188, 70);
  padding: .02rem;
  border-radius: .02rem;
}
.span8{
  background-color: rgb(240, 115, 115);
  padding: .02rem;
  border-radius: .02rem;
}
.dl2{
  font-size: 10px;
  display: flex;
  flex: 1;
  flex-direction: column;
  justify-content: space-around;

}
.xuxian{
  height: .2rem;
  display: flex;
  align-items: center;
}
em{
  width: 100%;
  height: -.091rem;
  border-top:.01rem dotted #999;
}
.huodong{
  width: 100%;
}
.zhekou{
  width: 75%;
  float: left;
}
.shou{
  margin-bottom:.08rem; 
}
.huo{
  float: right;
  width: 25%;
  text-align: right;
}
.koubei{
  margin: .1rem .1rem 0 0;
}
</style>
