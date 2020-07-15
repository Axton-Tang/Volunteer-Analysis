<template>
    <div>
        <el-dialog
            title="使用声明"
            :visible.sync="centerDialogVisible"
            width="30%"
            center
            :close-on-click-modal='false'
            :close-on-press-escape='false'
        >
            <span>需要注意的是内容是默认不居中的
                需要注意的是内容是默认不居中的
                需要注意的是内容是默认不居中的
                需要注意的是内容是默认不居中的
                需要注意的是内容是默认不居中的
            </span>
            <span slot="footer" class="dialog-footer">
                <el-button @click="closePage">取 消</el-button>
                <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
            </span>
        </el-dialog>

        <home-header></home-header>
        <home-title></home-title>
        <home-line-form @getLineData="getLineData" :showBackForm="showBackForm"></home-line-form>
        <home-line-table :linedata='linedata' :showAgainTable="showAgainTable" @backForm='backForm' @isGetMajor='isGetMajor'></home-line-table>
        <home-major-form id='strollToTable' :linedata='linedata' :majorGrade='majorGrade' @submitMajorForm='submitMajorForm'></home-major-form>
        <home-major-table :linedata='linedata' :majorValue='majorValue'></home-major-table>
        <home-footer></home-footer>
        <el-backtop :bottom='180' :right='70'></el-backtop>

    </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeTitle from './components/Title'
import HomeLineForm from './components/LineForm'
import HomeLineTable from './components/LineTable'
import HomeMajorForm from './components/MajorForm'
import HomeMajorTable from './components/MajorTable'
import HomeFooter from './components/Footer'

export default {
    name: 'Home', 
    components : {
        HomeHeader,
        HomeTitle,
        HomeLineForm,
        HomeLineTable,
        HomeMajorForm,
        HomeMajorTable,
        HomeFooter
    },
    data () {
        return {
            linedata: {},
            showAgainTable: false,
            showBackForm: false,
            majorGrade: '低',
            majorValue: '',
            centerDialogVisible: false
        }
    },
    methods: {
        closePage () {
            window.opener = null;
            window.open("about:blank", "_top").close()

        },
        getLineData (data) {
            this.showAgainTable = !this.showAgainTable
            this.linedata = data
        },
        backForm() {
            this.showBackForm = !this.showBackForm
            this.linedata = {}
        },
        isGetMajor (grade) {
            this.majorGrade = grade
        },
        submitMajorForm(value) {
            this.majorValue = value
            setTimeout( () => {
                document.querySelector("#strollToTable").scrollIntoView(true);
            },500)
            
        }
    },
    mounted() {
        this.centerDialogVisible = true
    }
}
</script>

<style>

</style>