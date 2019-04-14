<template>
    <div class="question-box-comp">
        <b-jumbotron>
            <template slot="lead">
                 {{question.question}}
            </template>

            <hr class="my-4">

            <b-container class="bv-example-row">
              <b-row >
                <b-col sm='6' offset='3'>list of answer</b-col>
              </b-row>
            </b-container>

            <b-button variant="primary" href="#">Submit</b-button>
            <b-button variant="success" href="#">Next</b-button>
        </b-jumbotron>
    </div>
</template>
<script>
export default {
  name: "",
  props:{
    question: Object  
  },
  data: () => ({

  })
}
</script>
<style lang="scss" scoped>
</style>
