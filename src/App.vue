<template>
  <div id="app">
    <AppHeader />
    <QuestionBox
        :question="questions[index]"
    />
  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
export default {
    name: 'app',
    data(){
        // return obj
        return {
            questions: null,
            index:0
        }
    },
    components: {
        'AppHeader': Header,
        QuestionBox
    },
    mounted () {
        axios
            .get('https://opentdb.com/api.php?amount=12&category=18&type=multiple')
            .then(response => response.data)
            .then(data => {
                this.questions = data.results
            })
        }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
