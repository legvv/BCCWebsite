<template>
    <div class="container">
        <ul class="container-nav">
            <nuxt-link :to="{name:'index'}" tag="li">
                Home
            </nuxt-link>
            <nuxt-link :to="{name:'educator'}" tag="li">
                Teaching Center
            </nuxt-link>
            <transition-group name="list">
                <nuxt-link tag="li" :class="index===currentPath.length-1&&'active'" :to="{name:path.url}"
                           :key="path.name" v-for="(path,index) in currentPath">
                    {{path.name}}
                </nuxt-link>
            </transition-group>
        </ul>
        <ul class="container-left-entries">
            <li :class="curActiveEntry==='myClass'&&'entries-active'">
                <nuxt-link :to="myClass" class="entries-container" tag="div"><i class="icon-course"></i><em
                        class="entries-name">My Class</em>
                </nuxt-link>
            </li>
            <li :class="curActiveEntry==='performance'&&'entries-active'">
                <nuxt-link :to="performance" class="entries-container" tag="div"><i class="icon-performance"></i><em
                        class="entries-name">Performance</em>
                </nuxt-link>
            </li>
            <li :class="curActiveEntry==='tools'&&'entries-active'">
                <nuxt-link :to="tools" class="entries-container" tag="div"><i class="icon-tools"></i><em
                        class="entries-name">Tools</em>
                </nuxt-link>
            </li>
        </ul>
        <article class="container-main">
            <nuxt-child></nuxt-child>
        </article>
    </div>
</template>
<script>
    import {mapState} from 'vuex'
    export default {
        asyncData({route, redirect}){
            const defaultPage = `/educator/myClass`;
            if (route.path === "/educator") {
                redirect(defaultPage);
            }
        },
        fetch({store}){
            const DEFAULT_ENTRY = "myClass";
            store.dispatch('index/educator/educator/changeEntryActive', DEFAULT_ENTRY);
        },
        data () {
            return {
                myClass: {name: 'educator-myClass'},
                performance: {name: 'educator-performance'},
                tools: {name: 'educator-tools'},
            }
        },
        methods: {},
        created(){
        },
        computed: {
            ...mapState('index/educator/educator', {
                curActiveEntry: state => state.curActiveEntry,
                currentPath: state => state.currentPath
            })
        },
        components: {}
    }
</script>
<style lang="less" scoped>
    @import "~~assets/less/element/main_container";

    .main-content {
        width: 10.13rem;
        padding: .18rem .28rem;
        background: white;
        overflow: hidden;
    }

    .icon-course {
        width: 40px;
        height: 39px;
        background: url("~~assets/img/enties-icon/course.svg")no-repeat;
        background-size: 100% 100%;
    }

    .icon-performance {
        width: 41px;
        height: 40px;
        background: url("~~assets/img/enties-icon/Performance.svg") no-repeat;
        background-size: 100% 100%;
    }

    .icon-tools {
        width: 38px;
        height: 40px;
        background: url("~~assets/img/enties-icon/tools.svg") no-repeat;
        background-size: 100% 100%;
    }

    .entries-name {
        font-family: GothamRounded-Book;
        position: absolute;
        display: inline-block;
        margin: 10% 0 0 0;
        color: #5A6572;
        font-size: 14px;
        width: 100%;
        text-align: center;
        left: 0;
    }

    /*选中状态*/
    .entries-active {
        background: #425d82;
        .icon-course {
            width: 40px;
            height: 39px;
            background: url("~~assets/img/enties-icon/course-active.svg");
            background-size: 100% 100%;
        }
        .icon-performance {
            width: 41px;
            height: 40px;
            background: url("~~assets/img/enties-icon/Performance-active.svg") no-repeat;
            background-size: 100% 100%;
        }
        .icon-tools {
            width: 38px;
            height: 40px;
            background: url("~~assets/img/enties-icon/tools-active.svg") no-repeat;
            background-size: 100% 100%;
        }
        div > em {
            color: #ffffff;
        }
    }
</style>
