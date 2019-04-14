<template>
    <div class="question-box-comp">
        <b-jumbotron>
            <template slot="lead">
                 {{question.question}}
            </template>

            <hr class="my-4">

            <b-list-group>
                <b-list-group-item
                    v-for="(answer,index) in shuffledAnswers"
                    :key="index"
                    @click.prevent="selectAnswer(index)"
                    :class="[
                                !answered && selectedIndex === index ? 'selected':
                                 answered && correctIndex === index ? 'correct':
                                 answered && selectedIndex === index && correctIndex !== index ?
                                 'incorrect':''
                            ]"
                    >
                    {{answer}}
                </b-list-group-item>
            </b-list-group>

            <b-button
                variant="primary"
                @click.prevent="submitAnswer"
                :disabled="selectedIndex ===null || answered"
                >
            Submit</b-button>
            <b-button variant="success"
                @click.prevent="next"
                :disabled="quizHabis >=11"
                >Next</b-button>
            <hr class="my-4">
            <p>pilih salah satu jawaban diatas untuk enable submit button
            dan click next button untuk soal berikutnya</p>
        </b-jumbotron>
    </div>
</template>
<script>
import _ from 'lodash'
export default {
  name: "",
  props:{
    question: Object,
    next:Function,
    increment: Function,
    quizHabis: Number
  },
  data: () => ({
      selectedIndex:null,
      correctIndex: null,
      answered:false,
      shuffledAnswers:[]
  }),
  methods:{
      selectAnswer(index){
          this.selectedIndex=index;
      },
      submitAnswer(){
          let isCorrect=false;
          if(this.selectedIndex === this.correctIndex){
              isCorrect = true;
          }
          this.answered=true;
          this.increment(isCorrect);
      },
      shuffleAnswer(){
          let answers = [...this.question.incorrect_answers,this.question.correct_answer];
          this.shuffledAnswers = _.shuffle(answers)
          this.correctIndex = this.shuffledAnswers.indexOf(this.question.correct_answer);
      }
  },
  watch:{
      question:{
          immediate: true,
          handler(){
              this.selectedIndex=null;
              this.answered = false;
              this.shuffleAnswer();
          }
      }
  }
}
</script>
<style  scoped>
    .list-group{
        margin-bottom: 15px;
    }
    .list-group-item{
        cursor: pointer
    }
    .list-group-item:hover{
        background:#eee;
    }
    .btn{
        margin: 0 5px;
    }
    .selected{
        background: lightblue;
    }
    .correct{
        background: lightgreen;
    }
    .incorrect{
        background: purple;
    }
</style>
