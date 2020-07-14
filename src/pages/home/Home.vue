<template>
    <div>
        <home-header></home-header>
        <home-title></home-title>
        <home-line-form @getLineData="getLineData"></home-line-form>
        <home-line-table :linedata='linedata'></home-line-table>
    </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeTitle from './components/Title'
import HomeLineForm from './components/LineForm'
import HomeLineTable from './components/LineTable'

export default {
    name: 'Home', 
    components : {
        HomeHeader,
        HomeTitle,
        HomeLineForm,
        HomeLineTable
    },
    data () {
        return {
            linedata: ''
        }
    },
    methods: {
        getLineData (data) {
            this.linedata = data
        }
    }
}
</script>

<style>

</style>