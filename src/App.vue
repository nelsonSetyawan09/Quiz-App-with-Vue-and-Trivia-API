<template>
  <div id="app">
    <AppHeader
        :numCorrect="numCorrect"
        :numTotal="numTotal"
    />
    <b-container class="bv-example-row">
      <b-row >
        <b-col
            sm='6'
            offset='3'>
            <QuestionBox
                v-if="questions.length"
                :question="questions[index]"
                :next="next"
                :increment="increment"
                :quizHabis="index"
            />
        </b-col>
      </b-row>
    </b-container>

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
            questions: [],
            index:0,
            numCorrect:0,
            numTotal:0
        }
    },
    components: {
        'AppHeader': Header,
        QuestionBox
    },
    methods:{
        next(){
            this.index++
        },
        increment(isCorrect){
            if(isCorrect){
                this.numCorrect++;
            }
            this.numTotal++;
        }
    },
    mounted() {
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
