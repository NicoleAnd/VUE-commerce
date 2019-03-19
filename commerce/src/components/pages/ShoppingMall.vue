<template>
    <div>
        <div class="search-bar">
            <van-row>
                <van-col span="3">
                    <img class="location-icon" :src="locationIcon" />
                </van-col>
                <van-col span="16">
                    <input type="text" class="search-input" />
                </van-col>
                <van-col span="5">
                    <van-button size="mini">查找</van-button>
                </van-col>
            </van-row>
        </div>
        <!-- swiper area -->
        <div class="swiper-area">
            <van-swipe :autoplay="1000">
                <van-swipe-item v-for="(banner,index) in bannerPicArray" :key="index">
                    <img v-lazy="banner.image" width="100%">
                </van-swipe-item>
            </van-swipe>
        </div>
        <!-- type bar -->
        <div class="type-bar">
            <div v-for="(cate,index) in category" :key="index">
                <img v-lazy="cate.image" width="90%"/>
                <span>{{cate.mallCategoryName}}</span>
            </div>
        </div>
        <!-- adBanner area -->
        <div>
            <img v-lazy="adBanner" width="100%" />
        </div>
        <!-- Recommend goods area -->
        <div class="recommend-area">
            <div class="recommend-title">
                商品推荐
            </div>
            <div class="recommend-body">
                <swiper>
                    <swiper-slide>
                        <div class="recommend-item">
                            <img src="" width="80%" />
                            <div></div>
                            <div></div>
                        </div>
                    </swiper-slide>
                </swiper>
            </div>
        </div>
    </div>

</template>

<script>
    import axios from 'axios'
    import 'swiper/dist/css/swiper.css'
    import { swiper, swiperSlide } from 'vue-awesome-swiper'
    export default {
        data() {
            return {
                msg: 'Shopping Mall',
                locationIcon: require('../../assets/images/location.png'),
                bannerPicArray:[],
                category:[],
                adBanner:'',
                recommendGoods:[],
            }
        },
        components:{
            swiper,
            swiperSlide
        },
        created(){
            axios({
                url:'https://www.easy-mock.com/mock/5c8f8092aefa8c773573b5da/commerce/index',
                method:'get',
            })
            .then(res=>{
                console.log(res);
                if(res.status == 200){
                    let result = res.data.data;
                    this.category = result.category;
                    this.adBanner = result.advertesPicture.PICTURE_ADDRESS;
                    this.bannerPicArray = result.slides;
                    this.recommendGoods = result.recommend;
                }
            })
            .catch(error=>{
                console.log(error);
            })
        },
    }
</script>

<style scoped>
    .search-bar{
        height: 2.2rem;
        background-color: #e5017d;
        line-height: 2.2rem;
        overflow: hidden;
    }
    .location-icon{
        width: 50%;
        padding-top: .5rem;
        padding-left: .5rem;
    }
    .search-input{
        width: 100%;
        height: 1.3rem;
        border:0;
        border-bottom: 1px solid #fff!important;
        background-color: #e5017d;
        color:#fff;
    }
    .swiper-area{
        clear: both;
        max-height: 15rem;
        overflow: hidden;
    }
    .type-bar{
        background-color: #fff;
        margin: 0 .3rem .3rem .3rem;
        border-radius: .3rem;
        font-size: 14px;
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
    }
    .type-bar div{
        padding: .3rem;
        font-size: 12px;
        text-align: center;
    }
    .recommend-area{
        background-color: #fff;
        margin-top: .3rem;
    }
    .recommend-title{
        border-bottom: 1px solid #eee;
        font-size: 14px;
        padding:.2rem;
        color:#e5017d;

    }
</style>