<template>
    <div>
        <el-dialog
            title="使用协议"
            :visible.sync="centerDialogVisible"
            width="60%"
            center
            :close-on-click-modal='false'
            :close-on-press-escape='false'
            :show-close='false'
        >
            <h4>
                欢迎访问由“觅漾工作室”（以下简称为“我方”）出品的“中南林业科技大学2020高考志愿填报分析系统” （以下简称为“此系统”）。建议使用PC端进行访问。请您仔细阅读以下条款，如果您对本协议的任何条款表示异议，您可以选择不进入此系统。当您进入后，无论是否进行志愿分析，均意味着您（即「用户」）完全接受本协议项下的全部条款。
            </h4><br>
            <h3>一、定义</h3>
            <div>觅漾工作室： “觅漾工作室”前身为“林科大小可爱工作室”。是由中南林业科技大学学生自建的创新创业校园工作室。团队旨在丰富同学们的校园文化生活，提供便利的校园生活服务。同时，是大学生提升自我展现才能、开阔眼界的舞台。</div>
            <div>此系统 : 由“觅漾工作室” 技术部开发，旨在为高考后志愿填报的学生提供录取概率的参考。由于各省份高考政策的不同，以及新高考的实行，部分省份此前录取信息参考价值不大，故此系统仅支持 19 个省份的志愿分析。</div>
            <h3>二、免责声明</h3>
            <div>1、 本系统完全由我方开发，团队的学长学姐只是想为各位考生提供一些帮助。与中南林业科技大学招生办及任何其他组织无关！</div>
            <div>2、 本系统为无偿为考生服务，绝不收取任何费用。如有人假借我方名义对志愿分析进行收费，请广大考生及家长谨防上当受骗。</div>
            <div>3、 系统对考生信息进行分析后所得出的录取概率仅供参考，我方不对录取与否负任何责任！</div>
            <h3>三、个人隐私</h3>
            <div>我方重视个人信息保护，在您使用我方提供的服务时，您同意我方按照相关法律法规的规定收集、存储和保护您的个人信息。我方非经您的许可或根据相关法律、法规的强制性规定，不会透露您的个人信息。</div>
            <h3>四、其他</h3>
            <div>1、 本协议各条款标题仅为方便参阅而设，并不以任何方式界定、限制、解释或描述该条款的范围或限度。</div>
            <div>2、 本协议解释权及修订权归我方所有。</div>
            <div>3、 如果不同意我方对本协议相关条款所做的修改，用户有权并应当停止使用此系统。如果用户继续使用此系统，则视为用户接受我方对本协议相关条款所做的修改。</div>
            
            <span slot="footer" class="dialog-footer">
                <el-button @click="closePage">不 同 意</el-button>
                <el-button type="primary" @click="centerDialogVisible = false">同 意</el-button>
            </span>
        </el-dialog>
        <div class="code-wrapper" v-show='showCode' @click="closeCode">
            <img class="code-img" src="https://volunteer-analysis.oss-cn-shenzhen.aliyuncs.com/home/%E6%96%B0%E7%94%9F%E7%BE%A4.jpg">
        </div>
        <home-header></home-header>
        <home-title></home-title>
        <home-line-form @getLineData="getLineData" :showBackForm="showBackForm"></home-line-form>
        <home-line-table :linedata='linedata' :showAgainTable="showAgainTable" @backForm='backForm' @isGetMajor='isGetMajor'></home-line-table>
        <home-major-form id='strollToTable' :linedata='linedata' :majorGrade='majorGrade' @submitMajorForm='submitMajorForm'></home-major-form>
        <home-major-table :linedata='linedata' :majorValue='majorValue'></home-major-table>
        <home-solution></home-solution>
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
import HomeSolution from './components/Solution'
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
        HomeSolution,
        HomeFooter,
    },
    data () {
        return {
            linedata: {},
            showCode: true,
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
        closeCode () {
            this.showCode = false
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

<style lang="stylus" scoped>
    .code-wrapper
        position fixed
        left 0
        bottom 200px
        width 129px
        height 150px
        z-index 100
        .code-img
            width 100%
            height 100%
</style>