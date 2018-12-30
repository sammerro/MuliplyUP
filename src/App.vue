<template>
  <div class="container">

    <header class="header">
      <h1 class="header__title">
        MultiplyUP!
      </h1>
      <h2 class="header__subtitle">
        App for improving and training your multiplying ability.
      </h2>
    </header>
    <main class="main">
      <component :is="mode" @nexted="mode='app-question'" @answerChosen="answerChosen">

      </component>
      <button @click="(mode=='app-result')?mode='app-question':mode='app-result'">ZMIEN</button>
    </main>

  </div>
</template>

<script>
import AppResult from './components/AppResult.vue';
import AppQuestion from './components/AppQuestion.vue';

//504 017 371
export default {
  data() {
    return {
      mode: 'app-result'
    }
  },
  components: {AppResult, AppQuestion},
  methods: {
    answerChosen(ifCorrect) {
      if (ifCorrect ) {
        this.mode = 'app-result'
      } else {
        alert("bad answer. Try one more time.")
      }
    }

  }
}
</script>

<style lang="scss">
@import './styles/normalize.css';
:root {
  box-sizing: border-box;
  font-size: calc( 16px + (20 - 16) * ( (100vw - 300px) / ( 900 - 300) ));
  --primary-color: #344523;
}
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

//overwrite user agent and normalize

</style>

