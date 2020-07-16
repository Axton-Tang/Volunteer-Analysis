<template>
    <div class="header-wrapper">
        <div class="content-wrapper">
            <div class="message1">Copyright © 2018 - 2020 觅漾工作室 All Rights Reserved.</div>
            <div class="message2">湖南庠序文化传媒有限公司&nbsp;&nbsp;&nbsp;觅漾工作室&nbsp;&nbsp;&nbsp;旗下产品 &nbsp;&nbsp;&nbsp;
                开发者 : 技术部 <span style="color:#409EFF" @click="ClickDeveloper"> Axton Tang</span></div>
            <div class="icon-wrapper">
                <el-popover class="icon"
                    title="扫一扫了解更多资讯"
                    placement="top"
                    width="70"
                    trigger="click"
                >
                    <span class="iconfont" slot="reference">&#xe602;</span>
                    <div class="title" slot="reference">官方公众号</div>
                    <img src="https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E5%85%AC%E4%BC%97%E5%8F%B7%E4%BA%8C%E7%BB%B4%E7%A0%81.jpg" alt="微信公众号">
                </el-popover>

                <el-popover class="icon"
                    title="扫一扫了解更多资讯"
                    placement="top"
                    width="70"
                    trigger="click"
                >
                    <span class="iconfont" slot="reference">&#xe6c8;</span>
                    <div class="title" slot="reference">官方QQ</div>
                    <img src="https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/QQ%E4%BA%8C%E7%BB%B4%E7%A0%81.jpg" alt="官方QQ">
                </el-popover>

        </div>
        </div>

    </div>
</template>

<script>

export default {
    name: 'HomeFooter',
    methods: {
        ClickDeveloper() {
            this.$alert('axton-tang@lkdxka.com', '有问题请联系邮箱', {
            confirmButtonText: '确定',
            });
        }
    }

}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'

    .header-wrapper
        display flex
        flex-direction column
        align-items center
        margin-top 80px
        height 150px;
        background #fff
        background  #F8FAFC
        box-shadow: 0 -2px 8px 0 rgba(0, 0, 0, 0.1)
        .content-wrapper
            position relative
            height 100%
            width 1200px
            color #99a1a6
            line-height 40px
            font-size 14px
            .message1
                margin-top 40px
            .icon-wrapper
                position absolute
                right 0
                top 50%
                transform translateY(-50%)
                .icon
                    float left 
                    position relative
                    .title
                        position absolute
                        right -15px
                        line-height 15px
                    .iconfont
                        font-size 35px
                        margin-left 80px
                        color #D0D6D9
</style>
