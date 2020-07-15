<template>
    <div class="wrapper" v-if='showEnterMajor'>
        <div class="content-wrapper">
            <h1 style="margin-top:40px;color:#333">专业被调剂率分析</h1>
            <div class="title-wrapper">
                <div class="title-one">专业被调剂率 <i class="el-icon-question"></i></div>
                <div class="title-weo">重要提示</div>
            </div>
            
            <div class="header-wrapper">
                <div class="grade-progress">
                    <div class="gradeStyle">{{grade}}</div>
                    <el-progress type="dashboard" text-inside='' :percentage="percentage" :color="colors"></el-progress>
                </div>
                <div class="tips-wrapper">
                    <p class="tips">
                        文字是人类用表义符号记录表达信息以传之久远的方式和工具。现代文字大多是记录语言的工具。人类往往先有口头的语言后产生书面文字，很多小语种，有语言但没有文字。文字的不同体现了国家和民族的书面表达的方式和思维不同。文字使人类进入有历史记录的文明社会。文字按字音和字形，可分为表形文字、表音文字和
                    </p>
                </div>
            </div>
            <div class="border"></div>
            <div class="admission-title">
                <div style="color:#333;font-weight:500">2020&nbsp;</div>
                <div>{{this.linedata.radio1}}</div>&nbsp;
                <div>{{this.linedata.radio2}}</div>
                该专业招生计划
            </div>
            <el-table class="table-content"
                :data="tableData"
                style="width: 80%">
                <el-table-column
                    prop="smajor"
                    label="专业"
                    width="220">
                </el-table-column>
                <el-table-column
                    prop="plancount"
                    label="招生人数"
                    width="220">
                </el-table-column>
                <el-table-column
                    prop="money"
                    label="学费(元/年)"
                    width="220">
                </el-table-column>
                <el-table-column
                    prop="remarks"
                    label="备注"
                    width="260">
                </el-table-column>
            </el-table>
            
        </div>
        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HomeMajorTable',
    props : ['linedata', 'majorValue'],
    data () {
        return {
            showEnterMajor:false,
            tableData: [],
            percentage: 0,
            colors: [
            {color: '#f56c6c', percentage: 20},
            {color: '#e6a23c', percentage: 40},
            {color: '#5cb87a', percentage: 60},
            {color: '#1989fa', percentage: 80},
            {color: '#6f7ad3', percentage: 100}
            ],
            grade: ''
        }
    },
    methods: {

        submitForm () {
            
            axios.get('http://localhost:8000/api/lookup/entermajor?province='+this.linedata.radio1+ '&subject=' +this.linedata.radio2+ '&smajor=' +this.majorValue+'&score='+this.linedata.num2)
                .then(this.getHomeInfoSucc)
            axios.get('http://localhost:8000/api/lookup/majorsitu?province='+this.linedata.radio1+ '&subject=' +this.linedata.radio2+ '&smajor=' +this.majorValue)
                .then(this.getHomeInfoSucc2)
        },
        getHomeInfoSucc (res) {
            const gradeno = res.data.majorno
            if (gradeno === 10) {
                this.grade = '低'
                this.percentage = 30
            } else if (gradeno ===11) {
                this.grade = '高'
                this.percentage = 70
                
            } 
            this.showEnterMajor = true
        },
        getHomeInfoSucc2 (res) {
            res=res.data
            const data=res.data
            this.tableData = data
            this.$notify({
                title: '分析成功',
                message: '分析结果仅供参考！',
                type: 'success',
                offset: 100
            });
        }
    },
    watch: {
        majorValue () {
            this.submitForm()
        },
        linedata() {
            if(this.linedata.num1 == null) {
                this.showEnterMajor = false
            }
        }
    },

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
            display flex
            flex-direction column
            align-items center
            .title-wrapper
                width 950px
                text-align center
                font-size 22px
                margin 30px 0 0 0 
                font-weight 600
                color $bgColor
                .title-one
                    width 50%
                    float left
                    margin 0 auto
                    .el-icon-question
                        color #ccc
                .title-two
                    width 50%
                    float left
            .header-wrapper
                width 100%
                margin 30px 0
                .grade-progress
                    position relative
                    width 300px
                    margin 0 0 0 300px
                    float left
                    .gradeStyle
                        position absolute
                        left 50px
                        top 45px
                        font-size 25px
                .tips-wrapper
                    float left
                    word-wrap break-word
                    width 440px
                    margin 0 160px 0 0
            .border
                border 1px solid #F5F5F6
                width 900px
                margin 0 0 20px 0        
            .table-content
                margin 20px 50px 40px 50px
            .admission-title
                width 1200px
                position relative
                left 130px
                font-size 22px
            .admission-title div
                float left
                color $bgColor
                font-weight 600
</style>
