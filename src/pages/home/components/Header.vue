<template>
    <div class="header-wrapper">
        <div class="content-wrapper">
            <div class="img-wrapper">
                <img class="img" src="
                    https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E8%A7%85%E6%BC%BE%E5%B7%A5%E4%BD%9C%E5%AE%A4LOGO%E7%BD%91%E7%AB%99%E7%89%88.png" alt="觅漾工作室">
            </div>
            <p class="slogan">创新创业校园工作室</p>
        </div>
    </div>
</template>

<script>

export default {
    name: 'HomeHeader',

}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'

    .header-wrapper
        display flex
        flex-direction column
        align-items center
        height 80px;
        background #fff
        box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1)
        .content-wrapper
            position relative
            height 100%
            width 1200px
            margin 0 100px
            .img-wrapper
                position absolute
                top 50%
                transform translateY(-50%)
                width 177.2px
                height 50px
                .img
                    width 100%
                    height 100%
            .slogan
                position absolute
                top 50%
                transform translateY(-50%)
                right 0
                color #666
                font-size 20px
</style>
