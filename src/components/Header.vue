<template>
  <div class="header-comp">
        <b-nav tabs>
            <b-nav-item disabled><strong>Quiz App</strong> </b-nav-item>
            <b-nav-item disabled>Counter {{numCorrect}}/{{numTotal}}</b-nav-item>
        </b-nav>
  </div>
</template>
<script>
export default {
  name: "",
  props:['numCorrect','numTotal'],
  data: () => ({

  })
}
</script>
<style  scoped>
</style>
