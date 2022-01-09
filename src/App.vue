<template>
  <div id="app">
    <input type="text" @input="getAdvice($event)" :value="searchAdvice" />
    <ul v-if="searchAdvice.length">
      <li v-for="adviceItem in searchedAdvices" :key="adviceItem.id">
        {{ adviceItem.advice }}
      </li>
    </ul>
    <button @click="test">TEST</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      searchAdvice: '',
      searchedAdvices: [],
    };
  },
  methods: {
    test() {
      console.log(process.env)
    },
    async getAdvice(event) {
      if (event.target.value === ' ') {
        event.target.value = '';
      }
      this.searchAdvice = event.target.value;
      if (this.searchAdvice.length > 0) {
        const res = await fetch(
          `https://api.adviceslip.com/advice/search/${this.searchAdvice}`
        );
        const advices = await res.json();
        this.searchedAdvices = advices.slips;
      }
    },
  },
};
</script>

<style lang="scss">
body {
  background-color: darken(#00acdc, 15%);
}
</style>
