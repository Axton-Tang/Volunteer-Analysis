<template>
    <div class="wrapper" v-if='showForm'>
        <div class="content-wrapper">
            <div class="form-title">录取概率分析<span class="el-icon-question"></span></div>
            <el-form  inline :model="form" label-width="120px" class="line-Form">
                
                <el-form-item class="item-title" label="省份">
                    <el-radio-group v-model="form.radio1">
                        <el-radio-button label="湖南"></el-radio-button>
                        <el-radio-button class="province-item" v-for="item of provinceList1" :key="item.id" :label="item.province">{{item.province}}</el-radio-button><br>
                        <el-radio-button class="province-item" v-for="item of provinceList2" :key="item.id" :label="item.province">{{item.province}}</el-radio-button>
                        <el-radio-button disabled label="暂不支持其他省份！"></el-radio-button>
                    </el-radio-group>
                </el-form-item><br>

                <el-form-item label="类别">
                    <el-radio v-model="form.radio2" label="理科" border size="medium"></el-radio>
                    <el-radio v-model="form.radio2" label="文科" border size="medium"></el-radio>
                    <el-radio label="不支持文理科合并省份" disabled border size="medium"></el-radio>
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
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HomeLineForm',
    props : ['showBackForm'],
    data() {
        return {
            showForm: true,
            form : {
                radio1: '湖南',
                radio2: '理科',
                num1: 10000,
                num2: 550
            },
            provinceList1:[{
                'id':1,
                'province':'广东'
                },{
                'id':2,
                'province':'河北'
                },{
                'id':3,
                'province':'河南'
                },{
                'id':4,
                'province':'福建'
                },{
                'id':5,
                'province':'湖北'
                },{
                'id':6,
                'province':'江西'
                },{
                'id':7,
                'province':'安徽'
                },{
                'id':8,
                'province':'重庆'
                },{
                'id':9,
                'province':'广西'
                }],
            provinceList2:[{
                'id':10,
                'province':'辽宁'
                },{
                'id':11,
                'province':'陕西'
                },{
                'id':12,
                'province':'四川'
                },{
                'id':13,
                'province':'山西'
                },{
                'id':14,
                'province':'云南'
                },{
                'id':15,
                'province':'宁夏'
                },{
                'id':16,
                'province':'贵州'
                },{
                'id':17,
                'province':'青海'
                },{
                'id':18,
                'province':'吉林'
                }]
        }
    },
    methods: {
        submitForm (form) {
            this.$emit('getLineData', this.form)
            this.showForm = false
        }
    },
    watch: {
        showBackForm () {
            this.showForm = true
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
                    color #ccc
                    margin-left 20px
           .line-Form
                margin 40px
                .province-item
                    margin 5px 0
                .button
                    margin-left 60px
</style>
