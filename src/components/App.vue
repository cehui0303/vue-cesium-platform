<template>
    <div class="app-container">

        <!-- 在这里放一个 Header  -->
        <!--<mt-header fixed title="gis试验平台">-->
        <!--<span slot="left" @click="goBack" v-show="flag">-->
        <!--<mt-button icon="back">返回</mt-button>-->
        <!--</span>-->
        <!--</mt-header>-->
        <!-- 左侧导航区域 -->

        <Menu theme="dark" class="app-nav">
            <Submenu name="0">

                <template slot="title">
                    <router-link tag="span" to="/">
                        数字地球平台
                    </router-link>
                </template>
            </Submenu>
            <Submenu name="1">

                <template slot="title">
                    <Icon type="ios-paper" />
                    <router-link tag="span" to="/layer">
                        图层
                    </router-link>
                </template>

            </Submenu>
            <Submenu name="2">
                <template slot="title">

                    <router-link tag="span" to="/view">
                        <Icon type="md-eye" color="white" />
                        视角
                    </router-link>
                </template>
            </Submenu>
            <Submenu name="3">
                <template slot="title">

                    <router-link tag="span" to="/meature">
                        <Icon type="ios-people" />
                        量测
                    </router-link>

                </template>
            </Submenu>
            <Submenu name="3">
                <template slot="title">
                    <router-link tag="span" to="/terrain">
                        <Icon type="ios-people" />
                        地形
                    </router-link>

                </template>
            </Submenu>
            <Submenu name="4">
                <template slot="title">
                    <Icon type="ios-people" />

                    <router-link tag="span" to="/model">
                        三维
                    </router-link>
                </template>
            </Submenu>
            <Submenu name="5">
                <template slot="title">

                    <router-link tag="span" to="/mark">
                        <Icon type="md-flag" color="white" />
                        标注
                    </router-link>

                </template>
            </Submenu>
            <Submenu name="6">
                <template slot="title">

                    <router-link tag="span" to="/data">
                        <Icon type="md-folder" color="white" />
                        数据
                    </router-link>
                </template>
            </Submenu>
            <Submenu name="7">
                <template slot="title">

                    <router-link tag="span" to="/setting">
                        <Icon type="ios-settings-outline" color="white" />
                        设置
                    </router-link>
                </template>
            </Submenu>
        </Menu>

        <!-- 路由的容器 -->
        <div class="app-view">
            <transition class="app-view">
                <router-view></router-view>
            </transition>
        </div>


        <!-- 地球容器 -->
        <cesium-container></cesium-container>


    </div>
</template>


<script>
    import {mapGetters} from "vuex";
    import VueCesium from 'vue-cesium';


    import CesiumContainer from './subcomponents/CesiumContainer.vue';


    export default {
        data() {
            return {
                flag: true // 默认显示返回按钮
            };
        },
        methods: {
            goBack() {
                // 点击返回按钮，向后跳转
                this.$router.go(-1);
                console.log(this);
            },

        },
        created() {
            if (this.$route.path === "/home") {
                this.flag = false;
            } else {
                this.flag = true;
            }
//            console.log(this.$store.state);
//            this.$store.dispatch('setCesiumInstance');
//            console.log(this.$store.state.cesiumInstance);
            console.log('version' + VueCesium.version)
        },
        watch: {
            // 当页面刷新的时候，不会触发 watch 中监听的 路由地址的变化
            "$route.path": function (newVal, oldVal) {
                if (newVal === "/home") {
                    this.flag = false;
                } else {
                    this.flag = true;
                }
            }
        },
        computed: {
            ...mapGetters(["totalcount"])
        },
        components: {
            CesiumContainer
        }
    };
</script>

// 这里写的样式，要符合 scss 语法，并且，样式是 当前组件私有的，不会成为全局的样式，也不会应用给子组件
// 取消scope
<style lang="scss">

    html, body {
        width: 100%;
        height: 100%;
    }

    .app-container {
        width: 100%;
        height: 100%;
        display: flex;
        padding: 0px;
        
        overflow: hidden;

        .ivu-menu-vertical .ivu-menu-submenu-title-icon {

            opacity: 0;
        }

    .app-sub-container{
        position:relative;
        width:100%;
        height:100%;
    }

        .app-nav {


            width: 200px ! important;
            max-width: 200px;
            min-width: 200px;

        }
        .app-view {
            /*width:200px;
            height:100%;
            position:absolute;
            border:1px solid red;
            z-index:999;*/
        }

        a {
            text-decoration: none;
        }

        .router-link-active {
            text-decoration: none;
        }
    }

    // 动画效果相关的类样式
    .v-enter {
        opacity: 0;
        // 让即将进入的页面，向右偏移 100% 屏幕的宽度
        transform: translateX(100%);
    }

    .v-leave-to {
        opacity: 0;
        // 让即将进入的页面，向右偏移 100% 屏幕的宽度
        transform: translateX(-100%);
        position: absolute;
    }

    .v-enter-active,
    .v-leave-active {
        transition: all 0.4s ease;
    }


</style>
