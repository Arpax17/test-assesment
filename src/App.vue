<template>
  <div>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <Question1 />
    <Question2 />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Question1 from './components/Question1.vue'
import Question2 from './components/Question2.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    Question1,
    Question2
  }
}
</script>


