<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><b>Take Our Brand Knowledge Quiz</b></b-nav-item>
      <b-nav-item disabled><b>{{ numCorrect }} out of 4</b></b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  props: [
    'numCorrect'
  ]
}
</script>