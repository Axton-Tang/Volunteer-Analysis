<template>
    <div class="title-wrapper">
        <div class="content-wrapper">
            <div class="img-wrapper">
                <img class="img" src="
                   https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E4%B8%AD%E5%8D%97%E6%9E%97%E4%B8%9A%E7%A7%91%E6%8A%80%E5%A4%A7%E5%AD%A6LOGO.png" alt="觅漾工作室">
            </div>
            <p class="title">2020高考志愿填报分析系统</p>
        </div>
    </div>
</template>

<script>

export default {
    name: 'HomeTitle',

}
</script>

<style lang="stylus" scoped>
    @import '~@/assets/styles/varibles.styl'

    .title-wrapper
        display flex
        flex-direction column
        align-items center
        height 250px;

        .content-wrapper
            position relative
            height 100%
            width 1200px
            margin 0 100px
            .img-wrapper
                position absolute
                top 50px
                left 50%
                transform translateX(-50%)
                width 306.8px
                height 70px
                .img
                    width 100%
                    height 100%
            .title
                position absolute
                left 50%
                top 150px
                transform translateX(-50%)
                color $bgColor
                font-size 35px
                letter-spacing 5px
                font-weight 600
</style>
