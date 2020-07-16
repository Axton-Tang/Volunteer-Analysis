<template>
    <div class="wrapper">
        <div class="content-wrapper">
            <div class="title">Q & A <span style="color:#ccc;font-size:20px">（非录取相关）</span></div>
            <div class="collapse">
                <el-collapse v-model="activeName" accordion>
                    <el-collapse-item v-for="item of solutions" :key="item.id" :title="item.questions" :name="item.id">
                        <div>{{item.answer}}</div>
                    </el-collapse-item>
                </el-collapse>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'HomeSolution',
    data() {
        return {

            activeName: '1',
            solutions: []
        }
    },
    methods: {
        getSolutions () {
            axios.get('http://localhost:8000/api/lookup/solutions')
                            .then(this.getHomeInfoSucc)
            
        },
        getHomeInfoSucc (res) {
            res=res.data
            const data=res.data
            this.solutions = data
        }
    },
    mounted() {
        this.getSolutions()
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
            .title
                margin 40px 0 0 40px
                font-size 28px
            .collapse
                width 80%
                margin 0 auto
                padding 40px 0
</style>
