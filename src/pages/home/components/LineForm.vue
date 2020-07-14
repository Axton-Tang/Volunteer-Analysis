<template>
    <div class="wrapper" v-if='showForm'>
        <div class="content-wrapper">
            <div class="form-title">录取概率分析<span class="el-icon-question"></span></div>
            <el-form  inline=true :model="form" label-width="120px" class="line-Form">
                
                <el-form-item class="item-title" label="省份">
                    <el-radio-group v-model="form.radio1">
                        <el-radio-button label="湖南"></el-radio-button>
                        <el-radio-button class="province-item" v-for="(item,index) of provinceList1" :key="index" :label="item">{{item}}</el-radio-button><br>
                        <el-radio-button class="province-item" v-for="(item,index) of provinceList2" :key="index" :label="item">{{item}}</el-radio-button>
                    </el-radio-group>
                </el-form-item><br>

                <el-form-item label="类别">
                    <el-radio v-model="form.radio2" label="理科" border size="medium"></el-radio>
                    <el-radio v-model="form.radio2" label="文科" border size="medium"></el-radio>
                </el-form-item><br>
                <el-form-item label="位次">
                   <el-input-number v-model="form.num1" :min="1" :max="100000" label="描述文字"></el-input-number>
                </el-form-item>
                <el-form-item label="分数">
                    <el-input-number v-model="form.num2" :min="200" :max="750" label="描述文字"></el-input-number>
                </el-form-item>
                <el-form-item class="button">
                    <el-button type="primary" @click="submitForm('form')">立即查询</el-button>
                </el-form-item>
            </el-form>
        </div>
        <div>{{test}}</div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HomeLineForm',
    data() {
        return {
            showForm: true,
            form : {
                radio1: '湖南',
                radio2: '理科',
                num1: 10000,
                num2: 550
            },
            provinceList1:['广东','河北','河南','福建','湖北','江西','安徽','重庆','广西'],
            provinceList2:['辽宁','陕西','四川','山西','云南','宁夏','贵州','青海','吉林'],
        }
    },
    methods: {
        submitForm (form) {
            this.$emit('getLineData', this.form)
            this.showForm = false
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
        .content-wrapper
            width 1200px
            box-shadow: 0 2px 12px 0 rgba(64, 158, 255, 0.3)
            .form-title
                margin 40px 0 0 40px
                font-size 28px
                .el-icon-question
                    font-size 25px
                    color #666
                    margin-left 20px
           .line-Form
                margin 40px
                .province-item
                    margin 5px 0
                .button
                    margin-left 60px
</style>
