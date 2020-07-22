<template>
    <div class="wrapper">
        <div class="more" v-show = "more" @click="ClickMore">点击了解更多 <span class="el-icon-arrow-down"></span></div>
        <el-collapse-transition>
        <div class="contents-wrapper" v-if="showMore">
            <div class="content-title"><span class="iconfont">&#xe63c;</span>了解林大</div>
            <div class="content-wrapper" @click="ClickOne">
                <div class="content content1">
                    <span class="iconfont">&#xe6d6;</span>
                    <img class="img" src="https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E9%82%82%E9%80%85.jpg" alt="">
                    <div class="info-wrapper">
                        <div class="title">邂逅林科大</div>
                        <div class="info">疫情之下的林科大显得有些冷清，我们在这里等你、迎你，<br>让校园重回生机！<br>感谢 视频拍摄：梁定坤 后期：龚永健</div>
                    </div>
                </div>
            </div>
            <div class="content-wrapper" @click="ClickTwo">
                <div class="content content2">
                    <span class="iconfont">&#xe6d6;</span>
                    <img class="img" src="https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E9%9B%A8%E6%A8%B1.jpg" alt="">
                    <div class="info-wrapper">
                        <div class="title">雨樱 · 林科大</div>
                        <div class="info">春天的林科大有多美呢？ 来吧，我想和你一起赏樱！<br> 感谢 视频制作人：uncleB （微信：17600161701）</div>
                    </div>
                </div>
            </div>
            <div class="content-wrapper" @click="ClickThree">
                <div class="content content3">
                    <span class="iconfont">&#xe6d6;</span>
                    <img class="img" src="https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E5%8D%B0%E8%B1%A1.jpg" alt="">
                    <div class="info-wrapper">
                        <div class="title">印象林科大</div>
                        <div class="info">“螺蛳粉职业技术学院” ？ 对了，就是这里。听说你也喜欢螺蛳粉？<br>感谢 视频制作人：钢筋KUI （B站）</div>
                    </div>
                </div> 
            </div>
            <div class="content-wrapper" @click="ClickFour">
                <div class="content content4">
                    <span class="iconfont">&#xe6d6;</span>
                    <img class="img" src="https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/20%EF%BC%9A45.jpg" alt="">
                    <div class="info-wrapper">
                        <div class="title">24 : 05 长沙</div>
                        <div class="info">感受下长沙这座不夜城的魅力吧！ <br> 原色长沙 出品</div>
                    </div>
                </div>
            </div>

        </div>
        </el-collapse-transition>
        <div class="video-wrapper" v-if="showVideo" >
            <div class="back" @click="Close"></div>
            <video-player class="video-player vjs-custom-skin" ref="videoPlayer" :playsinline="true" :options="playerOptions"></video-player>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HomeVideo',
    data() {
        return {
            showMore: false,
            more: true,
            showVideo: false,
            playerOptions: {
                playbackRates: [0.7, 1.0, 1.5, 2.0], //播放速度
                autoplay: true, //如果true,浏览器准备好时开始回放。
                muted: false, // 默认情况下将会消除任何音频。
                loop: false, // 导致视频一结束就重新开始。
                preload: 'auto', // 建议浏览器在<video>加载元素后是否应该开始下载视频数据。auto浏览器选择最佳行为,立即开始加载视频（如果浏览器支持）
                language: 'zh-CN',
                aspectRatio: '16:9', // 将播放器置于流畅模式，并在计算播放器的动态大小时使用该值。值应该代表一个比例 - 用冒号分隔的两个数字（例如"16:9"或"4:3"）
                fluid: true, // 当true时，Video.js player将拥有流体大小。换句话说，它将按比例缩放以适应其容器。
                sources: [{
                    type: "video/mp4",
                    src: "" //视频url地址
                }],
                poster: "", //你的封面地址
                // width: document.documentElement.clientWidth,
                notSupportedMessage: '此视频暂无法播放，请稍后再试', //允许覆盖Video.js无法播放媒体源时显示的默认信息。
                controlBar: {
                    timeDivider: true,
                    durationDisplay: true,
                    remainingTimeDisplay: false,
                    fullscreenToggle: true  //全屏按钮
                }
            }
        }
    },
    methods :{
        ClickMore () {
            this.showMore = true
            this.more = false
        },
        ClickOne () {
            this.showVideo = true
            this.playerOptions.sources = {
                type: "video/mp4",
                src: "https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/video/%E9%82%82%E9%80%85%E6%9E%97%E7%A7%91%E5%A4%A7%EF%BC%88%E6%96%B0%EF%BC%89.mp4" //视频url地址
            }
            this.playerOptions.poster = 'https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E9%82%82%E9%80%85.jpg'
        },
        ClickTwo () {
            this.showVideo = true
            this.playerOptions.sources = {
                type: "video/mp4",
                src: "https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/video/%E9%9B%A8%E6%A8%B1%C2%B7%E6%9E%97%E7%A7%91%E5%A4%A7%EF%BC%88%E6%96%B0%EF%BC%89.mp4" //视频url地址
            }
            this.playerOptions.poster = 'https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E9%9B%A8%E6%A8%B1.jpg'
        },
        ClickThree () {
            this.showVideo = true
            this.playerOptions.sources = {
                type: "video/mp4",
                src: "https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/video/%E5%8D%B0%E8%B1%A1%E6%9E%97%E7%A7%91%E5%A4%A7.mp4" //视频url地址
            }
            this.playerOptions.poster = 'https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E5%8D%B0%E8%B1%A1.jpg'
        },
        ClickFour () {
            this.showVideo = true
            this.playerOptions.sources = {
                type: "video/mp4",
                src: "https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/video/24%EF%BC%9A05%E5%8E%9F%E8%89%B2%E9%95%BF%E6%B2%99.mp4" //视频url地址
            }
            this.playerOptions.poster = 'https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/20%EF%BC%9A45.jpg'
        },
        Close() {
            this.showVideo = false
        }
    }
}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'
    .wrapper
        display flex
        flex-direction column
        align-items center
        margin-bottom 50px
        .more
            font-size 20px
            color #666
        .video-wrapper
            .back
                position fixed
                top 0
                left 0
                bottom 0
                left 0
                width 100%
                height 100%
                z-index 100
                overflow hidden
                background rgba(0,0,0,0.3)
            .video-player
                position fixed
                top 50%
                left 50%
                transform translate(-50%,-50%)
                z-index 200
                width 1200px
        .contents-wrapper
            width 1200px
            margin 0 100px
            .iconfont
                font-size 25px
                margin-right 5px
                color $bgColor
            .content-title
                margin 0 0 40px 40px
                font-size 28px
            .content-wrapper
                float left
                width 600px
                height 500px
                background #fff
                .content
                    position relative
                    width 570px
                    height 470px
                    border-radius 20px
                    box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1)

                    .iconfont
                        position absolute
                        top 150px
                        left 50%
                        transform translateX(-50%)
                        font-size 60px
                        color rgba(255,255,255,0.5)
                    .img
                        width 570px
                        border-top-left-radius 20px
                        border-top-right-radius 20px
                    .info-wrapper
                        margin 20px
                        .title
                            font-size 25px
                            color #333
                        .info
                            margin 10px 0
                            color #666
                            word-wrap break-word
                .content2
                    float right
                .content3
                    margin-top 30px
                .content4
                    float right 
                    margin-top 30px

</style>
