<template>
    <div class="wrapper" v-if = 'showMajorForm'>
        <div class="content-wrapper">
            <div class="form-title">专业被调剂率分析<span class="el-icon-question"></span></div>
            <el-form inline label-width="120px" class="line-Form">
                
                <el-form-item class="item-title" label="专业">
                    <el-select v-model="value" filterable clearable placeholder="请选择">
                        <el-option
                        v-for="item in options"
                        :key="item.smajor"
                        :label="item.smajor"
                        :value="item.smajor">
                        </el-option>
                    </el-select>
                </el-form-item>

                <el-form-item class="button">
                    <el-button type="primary" @click="submitMajorForm('value')">立即查询</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HomeMajorForm',
    props : ['linedata', 'majorGrade'],
    data() {
        return {
            showMajorForm: false,
            options: [],
            value: ''
        }
    },
    methods: {
        getMajor () {
            axios.get('http://localhost:8000/api/lookup/major?province='+this.linedata.radio1+ '&subject=' +this.linedata.radio2)
                            .then(this.getHomeInfoSucc)
            
        },
        getHomeInfoSucc (res) {
            res=res.data
            const data=res.data
            this.options = data
        },
        submitMajorForm (value) {
            this.$emit('submitMajorForm', this.value)
        }
    },
    watch: {
        linedata () {
            if(this.linedata.num1 == null) {
                this.showMajorForm = false
                this.value = ''
            }

            setTimeout( () => {
                if (this.linedata.num1 && this.majorGrade !== '低') {

                    this.getMajor()
                    this.showMajorForm = true
                    
                } 
            },2000)
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
