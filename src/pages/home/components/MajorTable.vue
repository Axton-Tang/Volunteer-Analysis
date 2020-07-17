<template>
    <div class="wrapper" v-if='showEnterMajor'>
        <div class="content-wrapper">
            <h1 style="margin-top:40px;color:#333">专业被调剂概率分析</h1>
            <div class="title-wrapper">
                <div class="title-one">专业被调剂概率 
                    <el-popover
                        placement="right"
                        title="专业被调剂概率说明"
                        width="350"
                        trigger="click"
                    >
                        <div>“高” ：被调剂到其他专业的可能性很大 </div>
                        <div>“低” ：基本上能够进入此专业 </div>
                        <i class="el-icon-question" slot="reference"></i>
                    </el-popover>
                </div>
                <div class="title-weo">重要提醒</div>
            </div>
            
            <div class="header-wrapper">
                <div class="grade-progress">
                    <div class="gradeStyle">{{grade}}</div>
                    <el-progress type="dashboard" text-inside='' :percentage="percentage" :color="colors"></el-progress>
                </div>
                <div class="tips-wrapper">
                    <div>1、 只有当学校录取概率为“中”及以上的考生，才能够显示专业被调剂概率分析</div> <br>
                    <div>2、 专业被调剂概率的是在学校录取概率的基础上分进行析的，
                        而学校录取概率可能就具有一定偏差，故专业被调剂概率的偏差可能更大，仅供参考！</div><br>
                    <div>3、 各省份各专业的招生计划只考虑“普通类”</div>
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
            {color: '#6f7ad3', percentage: 20},
            {color: '#1989fa', percentage: 40},
            {color: '#5cb87a', percentage: 60},
            {color: '#e6a23c', percentage: 80},
            {color: '#f56c6c', percentage: 100}
            ],
            grade: ''
        }
    },
    methods: {

        submitForm () {
            
            axios.get('http://149.129.116.64:3000/api/lookup/entermajor?province='+this.linedata.radio1+ '&subject=' +this.linedata.radio2+ '&smajor=' +this.majorValue+'&score='+this.linedata.num2)
                .then(this.getHomeInfoSucc)
            axios.get('http://149.129.116.64:3000/api/lookup/majorsitu?province='+this.linedata.radio1+ '&subject=' +this.linedata.radio2+ '&smajor=' +this.majorValue)
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
            if (this.tableData) {
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
            border-radius 20px
            display flex
            flex-direction column
            align-items center
            margin 0 100px
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
