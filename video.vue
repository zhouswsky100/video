<template>
    <div class="video" >
        <div v-for="(item,index) in videoList " :key="index" >
            <div class="onbox"  v-if="getDevice()!=1">
                 <div class="box"  @click="onClick(index)" ></div>
            </div>
            <div class="video-box" >
                <video
                    :id="'video' + index"
                    :ref="'video'+ index"
                    class="video"
                    :src="getSrc(item.src)"
                    :poster="getSrc(item.poster)"
                    type="video/mp4"  
                    controls
                    :playsinline="true"
                     x5-video-player-type="h5-page"
                    :webkit-playsinline="true"
                    :x5-playsinline="true"
                    >
                    <source class="source" type="video/mp4"/>
                </video>
            </div>
            <p class="vtxt">{{item.title}}</p>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        videoList: {
            type: Array,
        },
    },
    data() {
        return {
            player:null,
            videoFlg:false,
        }
    },
    methods: {
        getDevice() {
            let u = navigator.userAgent;
            let isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1; //g
            let systemType = 0
            let isIOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
            if (isAndroid) {
                systemType = 2
            }
            if (isIOS) {
            　　systemType = 1
            }
            return systemType;
        },
        onClick(val) {
                this.player = this.$refs[`video${val}`][0];
                this.videoFlg = this.player.paused;
                this.videoList.forEach((item,index) => {
                    this.$refs[`${'video' + index}`][0].pause();
                });
                if(this.player.paused && this.videoFlg) {
                    this.player.play();
                } else {
                    this.player.pause();
                }
        },
        getSrc(src){
            return require(`@/assets` + src)
        }
    },
}
</script>

<style lang="less" scoped>
.video{
    .onbox{
        opacity: 0;
        position: relative;
        z-index: 1;
    }
    .box{
        position: absolute;
        height: 140px;
        width: 100%;
    }
    .vtxt{
        color: #323333;
        font-size: 14px;
        text-align: center;
    }
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
            object-position: center;
        }
        .time {
            color: #fff;
            font-size: 13px;
            right: 20px;
            bottom: 20px;
            position: absolute;
        }
    }
}
</style>
