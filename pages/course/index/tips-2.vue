<template>
    <div>
        <transition name="fade">
            <div class="style-3" v-if="true">
                <div class="course_common_box">
                    <div class="course-content">
                        <div v-for="item in tipsInfo.sentence">
                            <p :style="{'display':pinyinSwitch ? 'block':'none'}" class="en">{{item.pinyin||''}}</p>
                            <p class="cn">{{item.chinese}}</p>
                            <p class="en">{{item.english}}</p>
                        </div>
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
    import {mapState, mapActions, mapMutations} from 'vuex';
    import loadingImage from '~/components/loadingImage';
    export default {
        async fetch({isServer, redirect, store, params}){
            (isServer || !params) && redirect("/learner/myCourse");
            params.extendData || await store.dispatch("index/course/index/setContentInfo", params);
        },
        asyncData({params}){
            return {extendData: params.extendData}
        }, data () {
            return {}
        },
        methods: {
            ...mapActions('index/course/index', ['setTurningState', 'setBackbtnState']),
        },
        created () {
        },
        watch: {},
        computed: {
            contentInfo(){
                return this.courseExtendInfo || this.extendData || this.contentData;
            },
            ...mapState('index/course/index', {
                courseExtendInfo: state => state.courseExtendInfo,
                tipsInfo: state => JSON.parse(state.contentInfo.tips[0].content),
                templateStyle: state => state.templateStyle,
                pinyinSwitch: state => state.pinyinSwitch,
            }),
        },
        components: {
            loadingImage
        }
    }
</script>

<style lang="less" scoped>


</style>
