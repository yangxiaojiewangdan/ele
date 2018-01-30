<template>
  <div class="list">
    <div class="header">
      <div class="header-food">
        <mt-header title="美食">
          <router-link to="/" slot="left">
            <mt-button icon="back"></mt-button>
          </router-link>
        </mt-header>
      </div>
      <div class="header-screen">
        <a href="javascript" class="screen-nav">综合排序</a>
        <a href="javascript" class="screen-nav">距离最近</a>
        <a href="javascript" class="screen-nav">
          <i class="Member iconfont">&#xe692;</i>
          <span>会员领红包</span>
        </a>
        <a href="javascript" class="screen-nav-more">
          <span>筛选</span>
          <i class="screen iconfont">&#xe67f;</i>
        </a>
      </div>
    </div>
    <div class="from">
      <ul>
        <li class="from-li" v-for="item in list">
          <div class="from-left">
            <img class="from-img" :src="'https://fuss10.elemecdn.com/'+item.restaurant.image_path+'.'+item.restaurant.image_path.split('').slice(32,).join('')+'?imageMogr/format/webp/thumbnail/!130x130r/gravity/Center/crop/130x130/'">
          </div>
          <div class="from-right">
            <div class="introduce">
              <span>{{item.restaurant.name}}</span>
              <div class="right-star">
                <span>*****</span>
                <span>{{item.restaurant.rating}}</span>
                <span>
                  月售{{item.restaurant.recent_order_num}}单
                </span>
                <span class="from-Hummingbird">蜂鸟专送</span>
              </div>
              <div class="right-price">
                <span>
                  ￥{{item.restaurant.float_minimum_order_amount}}起送
                </span>
                <span>|</span>
                <span>配送费￥{{item.restaurant.float_delivery_fee}}</span>
                <div class="distance">
                  <span>1.36km</span>
                  <span>|</span>
                  <span>24分钟</span>
                </div>
              </div>
              <div class="evaluate">
                <img class="evaluate-img" :src="'https://fuss10.elemecdn.com/'+item.restaurant.recommend.image_hash+'.png?imageMogr/format/webp/thumbnail/!60x60r/gravity/Center/crop/60x60/'">
                <span class="evaluate-span">
                  {{item.restaurant.recommend.reason}}
                </span>
              </div>
            </div>
            <div class="Discount">
              <div class="reduce">
                <span class="reduce-first">
                  {{item.restaurant.activities[0].icon_name}}
                </span>
                <span>
                  {{item.restaurant.activities[0].tips}}
                </span>
              </div>
              <div class="gift">
               <!--  <span class="gift-reduce">
                  {{item.restaurant.activities[1].icon_name}}
                </span>
                <span class="full">
                  {{item.restaurant.activities[1].tips}}
                </span> -->
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'list',
  data () {
    return {
      list: []
    }
  },
  mounted () {
    var id = this.$route.params.id;
    axios.get('/restapi/shopping/v3/restaurants?latitude=39.90469&longitude=116.407173&keyword=&offset=0&limit=8&extras[]=activities&extras[]=tags&terminal=h5&brand_ids[]=&restaurant_category_ids[]=253&restaurant_category_ids[]=254&restaurant_category_ids[]=255&restaurant_category_ids[]=256&restaurant_category_ids[]=257&restaurant_category_ids[]=258&restaurant_category_ids[]=271&restaurant_category_ids[]=272&restaurant_category_ids[]=273&restaurant_category_ids[]=274&restaurant_category_ids[]=282&restaurant_category_ids[]=290&restaurant_category_ids[]=298')
    .then((res) => {
      console.log(res);
      this.list = res.data.items;
    })
  }
}
</script>

<style scoped>
  .header{
    position: fixed;
    width: 100%;
    height: 0.62rem;
    background: #009fff;
    z-index: 100;
  }
  .header-screen{
    display: flex;
    position: relative;
    height: 0.3rem;
    border-bottom: 1px solid #ddd;
    line-height: 0.3rem;
    z-index: 100;
    background: #fff;
  }
  .screen-nav{
    flex: 1;
    text-align: center;
    color: #666;
    position: relative;
    font-size: 0.11rem;
  }
  .Member{
    font-size: 0.08rem;
    color: #feca34;
  }
  .screen-nav-more{
    width: 0.64rem;
    height: 0.3rem;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #666;
    font-size: 0.11rem;
  }
  .screen{
    font-size: 0.1rem;
  }
  .from{
    position: relative;
    top: 0.75rem;
  }
  .from-li{
    overflow: hidden;
    border-bottom: 1px solid #fbfbfb;
  }
  .from-left{
    float: left;
  }
  .from-img{
    position: absolute;
    width: .58rem;
    height: .58rem;
    margin: .12rem;
  }
  .introduce{
    overflow: hidden;
    border-bottom: 1px solid #f4f4f4;
  }
  .from-right{
    float: left;
    font-size: .14rem;
    margin-top: .12rem;
    margin-left: .74rem;
  }
  .right-star{
    font-size: .1rem;
    width: 3rem;
  }
  .from-Hummingbird{
    font-size: .1rem;
    float: right;
    margin-right: .1rem;
    background: #009bff;
    color: #fff;
  }
  .right-price{
    font-size: .1rem;
  }
  .distance{
    float: right;
    margin-right: .1rem;
  }
  .evaluate{
    margin-bottom: .07rem;
  }
  .evaluate-img{
    width: .09rem;
    height: .09rem;
  }
  .evaluate-span{
    font-size: .06rem;
    color: #e8470b;
  }
  .Discount{
    margin-top: .1rem;
  }
  .reduce{
    font-size: .1rem;
  }
  .reduce-first{
    background: #70bc46;
    color: #fff;
  }
  .gift{
    font-size: .1rem;
  }
  .gift-reduce{
    background: #70bc46;
    color: #fff;
  }
  
</style>
