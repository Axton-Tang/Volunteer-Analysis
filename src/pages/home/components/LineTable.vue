<template>
    <div class="wrapper" v-if = 'showTable' v-loading="loading">
        <div class="content-wrapper">
            <el-popconfirm
                class="back"
                title="请不要频繁返回！"
                @onConfirm="handleBack"
                >
                <el-button slot="reference" >返回</el-button>
            </el-popconfirm>
            <h1 style="margin-top:40px;color:#">录取概率分析</h1>
            <div class="title-wrapper">
                <div class="title-one">录取概率 
                    <el-popover
                        placement="right"
                        title="录取概率说明"
                        width="350"
                        trigger="click"
                    >
                        <div>“极高” ：在不考虑考生身体状况等其他非成绩因素被退档的情况下,基本上可以被录取</div><br>
                        <div>“高” ：被录取的概率高 </div>
                        <div>“中” ：有一定概率被录取，但运气成分很大 </div>
                        <div>“低” ：基本上不会被录取 </div><br>
                        <div>“失败” ：表示系统分析失败，可能是系统不支持该省份科类分析,与考生所填信息无关！ </div>
                        <i class="el-icon-question" slot="reference"></i>
                    </el-popover>
                    </div>
                <div class="title-weo">重要提醒</div>
            </div>
            <div class="header-wrapper">
                <div class="grade-progress">
                    <div :class="gradeStyle">{{grade}}</div>
                    <el-progress type="dashboard" text-inside='' :percentage="percentage" :color="colors"></el-progress>
                </div>
                <div class="tips-wrapper">
                    <div>1、 录取概率的分析未考虑地方专项计划、国家专项计划、中外合作办学等招生类型。仅分析“普通类”的录取概率</div><br>
                    <div>2、 系统对考生信息进行分析后所得出的录取概率仅供参考，我方不对录取与否负任何责任！</div>
                </div>
            </div>
            <div class="border"></div>
            <div class="admission-title">
                <div>{{this.linedata.radio1}}</div>&nbsp;
                <div>{{this.linedata.radio2}}</div>
                历年录取情况
            </div>
            <el-table class="table-content"
                :data="tableData"
                style="width: 80%"
                >
                <el-table-column
                    prop="year"
                    label="年份"
                    width="180">
                </el-table-column>
                <el-table-column
                    prop="lowscore"
                    label="最低分"
                    width="180">
                </el-table-column>
                <el-table-column
                    prop="lowrank"
                    label="最低位次"
                    width="180">
                </el-table-column>
                <el-table-column
                    prop="type"
                    label="招生类型"
                    width="200">
                </el-table-column>
                <el-table-column
                    prop="batch"
                    label="录取批次"
                    width="200">
                </el-table-column>
            </el-table>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HomeLineTable',
    props : ['linedata', 'showAgainTable'],
    data () {
        return {
            showTable: false,
            tableData: [],
            percentage: 0,
            colors: [
            {color: '#f56c6c', percentage: 20},
            {color: '#e6a23c', percentage: 40},
            {color: '#5cb87a', percentage: 60},
            {color: '#1989fa', percentage: 80},
            {color: '#6f7ad3', percentage: 100}
            ],
            grade: '',
            gradeStyle: 'grade-one',
            loading: true
        }
    },
    methods: {
        handleBack() {
            this.showTable = false,
            this.tableData = []
            this.$emit('backForm')

        },
        submitForm () {
            
            axios.get('http://149.129.116.64:3000/api/lookup/line?province='+this.linedata.radio1+ '&subject=' +this.linedata.radio2+ '&rank=' +this.linedata.num1)
                .then(this.getHomeInfoSucc)
        },
        getHomeInfoSucc (res) {
            const gradeno = res.data.rankno
            if (gradeno === 1) {
                this.grade = '极高'
                this.percentage = 90
                this.gradeStyle = 'grade-one' ? 'grade-two' :'grade-one'
            } else if (gradeno ===2) {
                this.grade = '高'
                this.percentage = 70
                this.gradeStyle = 'grade-one'
                
            } else if (gradeno ===3) {
                this.grade = '中'
                this.percentage = 40
                this.gradeStyle = 'grade-one'
                
            } else if (gradeno ===4) {
                this.grade = '低'
                this.percentage = 10
                this.gradeStyle = 'grade-one'
               
            }
            else if (gradeno ===5) {
                this.grade = '失败'
                this.percentage = 0
                this.gradeStyle = 'grade-one' ? 'grade-two' :'grade-one'
               
            }
            res=res.data
            const data=res.data
            this.tableData = data
            this.showTable = true
            this.$emit('isGetMajor', this.grade)
            this.loading = false
            if (gradeno === 5) {
                this.$notify({
                    title: '分析失败',
                    message: '该省份科类不支持分析！',
                    type: 'error',
                    offset: 100
                });
            }
            else {
                this.$notify({
                    title: '分析成功',
                    message: '分析结果仅供参考！',
                    type: 'success',
                    offset: 100
                });
            }
        }
    },
    watch: {
        linedata () {
            if (this.linedata.num1) {
                this.submitForm()
            }   
        },
        showAgainTable () {
            this.showTable = true
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
            border-radius 20px
            display flex
            flex-direction column
            align-items center
            margin 0 100px
            .back
                position fixed
                font-size 20px
                left   0
                top 120px 
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
                    .grade-one
                        position absolute
                        left 50px
                        top 45px
                        font-size 25px
                    .grade-two
                        position absolute
                        left 40px
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
