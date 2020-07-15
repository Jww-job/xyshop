<template>

    <view class="home">
        <!--品牌导航-->
        <scroll-view class="scroll-view-list" scroll-x="true">
            <view class="scroll-view-item"
                  v-for="(item,index) in list"
                  :key="index"
                  @click="tabBarItemClick(index)"
                  :class="{active: index === currentIndex}">
                {{item}}
            </view>
        </scroll-view>
        <!--内容-->
        <scroll-view class="home-scroll-view-content"
                     id="1"
                     scroll-y="true"
                     @scroll="Scroll"
                     lower-threshold="100"
                     @scrolltolower="scrollToLower"
                     scroll-with-animation="200"
                     :scroll-top="scrollTop">
            <view class="content">
                <!--导航栏-->
                <view class="nav-list">
                    <view class="nav-item" v-for="(item, index) in navList[currentIndex]">
                        <view class="img"><image :src="item.icon"></image></view>
                        <view class="name">{{item.name}}</view>
                    </view>
                </view>

                <!--首发免单-->
                <view class="themes">

                    <view class="titles">
                        <text class="left">首发免单</text>
                        <text class="after"></text>
                        <text class="center">大牌正品 官方补贴</text>
                        <text class="right">更多</text>
                    </view>

                    <scroll-view class="themes-scroll-view-list" scroll-x="true">
                        <view class="themes-scroll-view-item"
                              v-for="(item,index) in themes[currentIndex]"
                              :key="index">
                            <view class="img"><image :src="item.img"></image></view>
                            <view class="name">{{item.name}}</view>
                        </view>
                    </scroll-view>

                </view>

                <!--商品显示-->
                <view class="goods">
                    <view class="goods-scroll-view-item"
                          v-for="(item,index) in goods[currentIndex]"
                          :key="index">
                        <view class="store-img"><image :src="item.img"></image></view>
                        <view class="goods-desc">
                            <view class="store">
                                <view class="store-left">
                                    <view class="store-name">
                                        <view class="name">{{item.title}}</view>

                                        <view class="tag-blue" v-show="item.tag === 1">{{item.tag | getMyTag(item.tag)}}</view>
                                        <view class="tag-green" v-show="item.tag === 2">{{item.tag | getMyTag(item.tag)}}</view>
                                        <view class="tag-orange" v-show="item.tag === 3">{{item.tag | getMyTag(item.tag)}}</view>

                                    </view>
                                    <view class="store-desc">
                                        <text class="sales">{{'已销售:' + item.sales + ' 件'}}</text>
                                        <text class="distance">{{item.distance + 'km'}}</text>
                                    </view>
                                </view>
                                <view class="store-right">
                                    <text class="go">去逛逛</text>
                                </view>
                            </view>
                            <view class="goods-list">
                                <view class="goods-item" v-for="(i, inx) in item.goods">
                                    <image :src="i.goods_img"></image>
                                </view>
                            </view>
                        </view>
                    </view>
                </view>

            </view>
        </scroll-view>
        <!--返回顶部-->
        <view class="show-top" v-show="isShowTop">
            <view class="img" @click="goTop">
                <image src="../../static/icon/top.png"></image>
            </view>
        </view>
    </view>

</template>

<script>

    export default {
        name: "home",
        data(){
            return {
                list: ['推荐','生活','奶茶','买车','购物','购物','购物','购物','购物','购物','购物','购物'],

                navList: {
                    '0': [
                        {
                            icon: require('../../static/icon/8.png'),
                            name: '限时秒杀',
                        },
                        {
                            icon: require('../../static/icon/6.png'),
                            name: '团购活动',
                        },
                        {
                            icon: require('../../static/icon/5.png'),
                            name: '特惠清仓',
                        },
                        {
                            icon: require('../../static/icon/1.png'),
                            name: '爱逛街',
                        },
                        {
                            icon: require('../../static/icon/3.png'),
                            name: '周边美食',
                        },
                        {
                            icon: require('../../static/icon/2.png'),
                            name: '生活便利',
                        },
                        {
                            icon: require('../../static/icon/7.png'),
                            name: '装修隔音',
                        },
                        {
                            icon: require('../../static/icon/10.png'),
                            name: '维修保养',
                        },
                        {
                            icon: require('../../static/icon/9.png'),
                            name: '医药馆'
                        },
                        {
                            icon: require('../../static/icon/4.png'),
                            name: '每日好店'
                        },
                    ],
                    '1': [
                        {
                            icon: require('../../static/icon/8.png'),
                            name: '限时秒杀',
                        },
                        {
                            icon: require('../../static/icon/6.png'),
                            name: '团购活动',
                        },
                        {
                            icon: require('../../static/icon/5.png'),
                            name: '特惠清仓',
                        },
                        {
                            icon: require('../../static/icon/1.png'),
                            name: '爱逛街',
                        },
                        {
                            icon: require('../../static/icon/3.png'),
                            name: '周边美食',
                        },
                        {
                            icon: require('../../static/icon/2.png'),
                            name: '生活便利',
                        },
                        {
                            icon: require('../../static/icon/7.png'),
                            name: '装修隔音',
                        },
                        {
                            icon: require('../../static/icon/10.png'),
                            name: '维修保养',
                        },
                        {
                            icon: require('../../static/icon/9.png'),
                            name: '医药馆'
                        },
                        {
                            icon: require('../../static/icon/4.png'),
                            name: '每日好店'
                        },
                    ],
                },
                themes: {
                    '0': [
                        {
                            img: require('../../static/goods/1.png'),
                            name: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                        },
                        {
                            img: require('../../static/goods/2.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/3.png'),
                            name: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                        },
                        {
                            img: require('../../static/goods/4.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/1.png'),
                            name: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                        },
                        {
                            img: require('../../static/goods/2.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/3.png'),
                            name: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                        },
                        {
                            img: require('../../static/goods/4.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/1.png'),
                            name: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                        },
                        {
                            img: require('../../static/goods/2.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/3.png'),
                            name: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                        },
                        {
                            img: require('../../static/goods/4.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                    ],
                    '1': [
                        {
                            img: require('../../static/goods/1.png'),
                            name: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                        },
                        {
                            img: require('../../static/goods/2.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/3.png'),
                            name: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                        },
                        {
                            img: require('../../static/goods/4.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/1.png'),
                            name: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                        },
                        {
                            img: require('../../static/goods/2.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/3.png'),
                            name: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                        },
                        {
                            img: require('../../static/goods/4.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/1.png'),
                            name: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                        },
                        {
                            img: require('../../static/goods/2.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                        {
                            img: require('../../static/goods/3.png'),
                            name: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                        },
                        {
                            img: require('../../static/goods/4.png'),
                            name: '2020年赫本风复古法式方肩宫廷日系温柔风长裙脚踝连衣裙子女夏',
                        },
                    ],

                },
                goods: {
                    '0': [

                        {
                            title: '夏2020新款女收腰显瘦气质女神范',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/clothing.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/clothing.png')},
                                {goods_img: require('../../static/goods/clothing.png')},
                                {goods_img: require('../../static/goods/clothing.png')},
                                {goods_img: require('../../static/goods/clothing.png')}
                            ]
                        },
                        {
                            title: '约会小裙子气质女神范衣服可甜可盐连衣裙女夏季',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/1.png'),
                            tag: 2,
                            goods: [
                                {goods_img: require('../../static/goods/1.png')},
                                {goods_img: require('../../static/goods/1.png')},
                                {goods_img: require('../../static/goods/1.png')},
                                {goods_img: require('../../static/goods/1.png')}
                            ]
                        },
                        {
                            title: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/2.png'),
                            tag: 3,
                            goods: [
                                {goods_img: require('../../static/goods/2.png')},
                                {goods_img: require('../../static/goods/2.png')},
                                {goods_img: require('../../static/goods/2.png')},
                                {goods_img: require('../../static/goods/2.png')}
                            ]
                        },
                        {
                            title: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/3.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/3.png')},
                                {goods_img: require('../../static/goods/3.png')},
                                {goods_img: require('../../static/goods/3.png')},
                                {goods_img: require('../../static/goods/3.png')}
                            ]

                        },
                        {
                            title: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/4.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/4.png')},
                                {goods_img: require('../../static/goods/4.png')},
                                {goods_img: require('../../static/goods/4.png')},
                                {goods_img: require('../../static/goods/4.png')}
                            ]

                        },
                        {
                            title: '楼下猪脚饭',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/phone.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/phone.png')},
                                {goods_img: require('../../static/goods/phone.png')},
                                {goods_img: require('../../static/goods/phone.png')},
                                {goods_img: require('../../static/goods/phone.png')}
                            ]
                        },

                    ],
                    '1': [

                        {
                            title: '夏2020新款女收腰显瘦气质女神范',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/clothing.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/clothing.png')},
                                {goods_img: require('../../static/goods/clothing.png')},
                                {goods_img: require('../../static/goods/clothing.png')},
                                {goods_img: require('../../static/goods/clothing.png')}
                            ]
                        },
                        {
                            title: '约会小裙子气质女神范衣服可甜可盐连衣裙女夏季',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/1.png'),
                            tag: 2,
                            goods: [
                                {goods_img: require('../../static/goods/1.png')},
                                {goods_img: require('../../static/goods/1.png')},
                                {goods_img: require('../../static/goods/1.png')},
                                {goods_img: require('../../static/goods/1.png')}
                            ]
                        },
                        {
                            title: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/2.png'),
                            tag: 3,
                            goods: [
                                {goods_img: require('../../static/goods/2.png')},
                                {goods_img: require('../../static/goods/2.png')},
                                {goods_img: require('../../static/goods/2.png')},
                                {goods_img: require('../../static/goods/2.png')}
                            ]
                        },
                        {
                            title: '约会小裙子气质女神范衣服可甜可盐赫本风小黑裙zmzf连衣裙女夏季',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/3.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/3.png')},
                                {goods_img: require('../../static/goods/3.png')},
                                {goods_img: require('../../static/goods/3.png')},
                                {goods_img: require('../../static/goods/3.png')}
                            ]

                        },
                        {
                            title: '2020年夏天显瘦赫本风可甜可盐长裙设计感小众牛仔开叉连衣裙子女',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/4.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/4.png')},
                                {goods_img: require('../../static/goods/4.png')},
                                {goods_img: require('../../static/goods/4.png')},
                                {goods_img: require('../../static/goods/4.png')}
                            ]

                        },
                        {
                            title: '楼下猪脚饭',
                            sales: 1000,
                            distance: 100,
                            img: require('../../static/goods/phone.png'),
                            tag: 1,
                            goods: [
                                {goods_img: require('../../static/goods/phone.png')},
                                {goods_img: require('../../static/goods/phone.png')},
                                {goods_img: require('../../static/goods/phone.png')},
                                {goods_img: require('../../static/goods/phone.png')}
                            ]
                        },

                    ],
                },
                currentIndex: 0,
                isShowTop: false,
                scrollTop: 0,
                old: {
                    scrollTop: 0
                }

            }

        },
        methods: {

            //tab-bar切换
            tabBarItemClick(index){

                console.log('index',index)
                this.currentIndex = index
            },

            //返回顶部
            goTop(){

                this.scrollTop = this.old.scrollTop

                this.$nextTick(() =>{
                    this.scrollTop = 0
                });

            },

            //监控滚动
            Scroll(e){

                this.old.scrollTop = e.detail.scrollTop
                this.old.scrollTop = e.detail.scrollTop
                if (this.old.scrollTop > 100){
                    this.isShowTop = true
                }else {
                    this.isShowTop = false
                }

            },

            //上拉加载更多
            scrollToLower(){

                let goods_list = [

                    {
                        title: '夏2020新款女收腰显瘦气质女神范',
                        sales: 1000,
                        distance: 100,
                        img: require('../../static/goods/clothing.png'),
                        tag: 1,
                        goods: [
                            {goods_img: require('../../static/goods/clothing.png')},
                            {goods_img: require('../../static/goods/clothing.png')},
                            {goods_img: require('../../static/goods/clothing.png')},
                            {goods_img: require('../../static/goods/clothing.png')}
                        ]
                    },
                    {
                        title: '夏2020新款女收腰显瘦气质女神范',
                        sales: 1000,
                        distance: 100,
                        img: require('../../static/goods/clothing.png'),
                        tag: 1,
                        goods: [
                            {goods_img: require('../../static/goods/clothing.png')},
                            {goods_img: require('../../static/goods/clothing.png')},
                            {goods_img: require('../../static/goods/clothing.png')},
                            {goods_img: require('../../static/goods/clothing.png')}
                        ]
                    }

                ]

                this.goods[this.currentIndex].push(...goods_list)

                console.log('1212')
            }
        },


        filters: {
            //tag过滤器
            getMyTag(tag){
                if (tag === 1){
                    return '旗舰店'
                }
                if (tag === 2){

                    return '直营店'
                }
                if (tag === 3){

                    return '官方'
                }
                if (tag === 4){

                    return '连锁'
                }
                if (tag === null){
                    return ''
                }
            }
        }
    }
</script>

<style scoped lang="less">
    .home{
        background-color: #f5f5f5;
    }
    .top-button{
        z-index: 200;
        position: fixed;
        bottom: 100px;
    }

    .scroll-view-list {
        white-space: nowrap;
        width: 100%;
        position: fixed;
        /*top: 40px;*/
        left: 0;
        z-index: 100;
        background-color: #FF3709;
    }

    .scroll-view-item {
        display: inline-block;
        width: 50px;
        height: 40px;
        line-height: 40px;
        text-align: center;
        font-size: 18px;
    }
    .home-scroll-view-content{
        position: relative;
        top: 40px;
        height: calc(100vh - 40px);
    }
    .content{
        .nav-list{
            display: flex;
            flex-wrap: wrap;
            text-align: center;
            background-color: white;
            .nav-item{
                width: 20%;
                padding: 10px 0;
                .img{
                    width: 100%;
                    height: 40px;
                    display: flex;
                    image{
                        margin: auto;
                        width: 40px;
                        height: 100%;
                    }
                }
                .name{
                    font-size: 14px;
                }

            }
        }
        .themes{
            margin: 10px 0;
            background-color: white;
            .titles{
                height: 40px;
                line-height: 40px;
                display: flex;
                margin: 0 10px;
                justify-content: space-between;
                font-size: 16px;
                .left{}
                .after{}
                .center{
                    color: #3F536E;
                }
                .right{}

            }
            .themes-scroll-view-list{
                white-space: nowrap;
                width: 100%;

                .themes-scroll-view-item{
                    display: inline-block;
                    width: 45%;
                    text-align: center;
                    font-size: 18px;
                    background-color: white;
                    .img{
                        width:100%;
                        height: 130px;
                        display: flex;
                        image{
                            margin: auto;
                            width: 90%;
                            height: 130px;
                            border-radius: 10px;
                        }
                    }
                    .name{
                        display: -webkit-box;

                        overflow: hidden;

                        text-overflow: ellipsis;

                        word-wrap: break-word;

                        white-space: normal !important;

                        -webkit-line-clamp: 1;
                        margin: 10px;
                        height: 20px;
                        font-size: 16px;

                    }

                }
            }
        }
        .goods{
            .goods-scroll-view-item{
                display: flex;
                margin: 10px 0;
                background-color: white;
                .store-img{
                    width: 30%;
                    margin: 10px 0 10px 5px;
                    height: 100px;
                    image{
                        width: 100%;
                        height: 100px;
                    }

                }
                .goods-desc{
                    flex: 1;
                    margin: 10px 5px;
                    .store{
                        height: 50%;
                        display: flex;
                        .store-left{
                            width: 70%;
                            .store-name{
                                display: flex;
                                height: 20px;
                                color: white;

                                .name{
                                    color: black;
                                    width: 120px;
                                    height: 100%;
                                    margin-right: 5px;
                                    overflow: hidden;
                                    font-size: 14px;
                                }
                                .tag-green{
                                    background-color: green;
                                    padding: 2px;
                                    font-size: 10px;
                                    border-radius: 3px;
                                }
                                .tag-blue{
                                    background-color: blue;
                                    padding: 2px;
                                    font-size: 10px;
                                    border-radius: 3px;
                                }
                                .tag-orange{
                                    background-color: orange;
                                    padding: 2px 10px;
                                    font-size: 10px;
                                    border-radius: 3px;
                                }
                            }
                            .store-desc{
                                font-size: 14px;
                                display: flex;
                                .sales{
                                    color: #8f8f94;
                                    margin-right: 10px;
                                }
                                .distance{
                                    color: blue;
                                }
                            }
                        }
                        .store-right{
                            width: 30%;
                            margin: 0 auto;
                            .go{
                                background-color: #FF3709;
                                padding: 5px 9px;
                                border-radius: 3px;
                                font-size: 16px;
                                color: white;
                            }
                        }


                        /*display: -webkit-box;*/
                        /*overflow: hidden;*/
                        /*text-overflow: ellipsis;*/
                        /*word-wrap: break-word;*/
                        /*white-space: normal !important;*/
                        /*-webkit-line-clamp: 3;*/
                        /*-webkit-box-orient: vertical;*/
                        /*height: 65px;*/
                        /*font-size: 16px;*/
                        /*color: black;*/
                    }
                    .goods-list{
                        display: flex;
                        height: 40%;
                        margin-top: 10px;
                        .goods-item{
                            margin: auto;
                            width: 23%;
                            height: 100%;
                            display: flex;
                            image{
                                margin: auto;
                                height: 100%;
                                width: 100%;
                            }
                        }

                    }

                }
            }

        }

    }
    .show-top{
        position: fixed;
        bottom: 100px;
        right: 20px;
        z-index: 200;
        .img{
            width: 40px;
            height: 40px;
            image{
                width: 100%;
                height: 100%;
            }
        }
    }
    .active{
        color: white;
        font-weight: 700;
    }

</style>