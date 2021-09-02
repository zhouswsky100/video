<template>
    <div class="video"  >
        <div class="onbox"  @click="onClick(0)" ></div>
        <div class="video-box" v-for="(item,index) in videoList " :key="index" >
            <video
                    :id="item.id"
                    :ref="item.ref"
                    class="video"
                    :src="item.src"
                    :poster="item.poster"
                     type="video/mp4"  
                    controls
                    :playsinline="true"
                    :webkit-playsinline="true"
                    :x5-playsinline="true"
                >
                <source class="source" type="video/mp4"/>
            </video>
        </div>
    </div>
</template>
<script>
import sendcode from '@/components/send-code.vue'

export default {
    components:{
        sendcode
    },
    props: {
        videoList: {
            type: Array,
            default:''
        },
    },
    data() {
        return {
            srcMom: require('@/assets/mom.mp4'),
            player:null,
            videoFlg:false,
        }
    },
    methods: {
          onClick(val) {
            if(getDevice()==2){
                this.player = this.$refs[`video${val}`];
                this.videoFlg = this.player.paused;
                const videoList = [0,1,2]
                videoList.forEach(item => {
                    this.$refs[`video${item}`].pause();
                });
                if(this.player.paused && this.videoFlg) {
                    this.player.play();
                } else {
                    this.player.pause();
                }
            }
        },
    },
}
</script>

<style lang="less" scoped>
.video{
    .video-box {
        width: 345px;
        border-radius: 5px;
        margin: 20px auto;
        position: relative;
        overflow: hidden;
        border: 1px solid #545454;
        .video {
            width: 100%;
            height: 100%;
            display: block;
            object-fit: contain;
            background-color: #242424;
        }
        .time {
            color: #fff;
            font-size: 13px;
            right: 20px;
            bottom: 20px;
            position: absolute;
        }
        .onbox{

        }
    }
}
</style>
