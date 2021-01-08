<template>
  <div id="app">
    <p class="title" v-html="title"></p>
    <p class="hits">Hits: {{ hits }}</p>
    <h1 :class="{ 'ok': isOk, 'ko': !isOk }" class="number">{{ number }}</h1>
    <button v-if="isOk" @click="setNumber">Another number!</button>
    <div>
      <input :disabled="isOk" class="binput" type="text" v-for="n in inputsQty" :key="n" @keyup="setBinary" maxlength="1">
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {  },
  data: function(){
    return {
      number: 0,
      binary: [],
      hits: -1
    }
  },
  computed: {
    inputsQty(){
      return this.number.toString('2').length
    },
    isOk(){
      return this.checkBinary()
    },
    title(){
      return 'Binary'.split('').map(l => '<span>' + l + '</span>' + l.charCodeAt(0).toString('2')).join(' ')
    }
  },
  methods: {
    checkBinary(){
      return this.binary.slice().join('') === this.number.toString('2')
    },
    setBinary(){
      this.binary = [...document.querySelectorAll('.binput')].map(e => e.value)
    },
    setNumber(){
      this.binary = []
      Array.from(document.querySelectorAll('.binput')).forEach(e => e.value = '')
      this.number = parseInt(Math.random() * (25 + this.hits), 10)
      this.hits++
    }
  },
  mounted(){
    this.setNumber()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 12px;
}
.binput, .number {
  max-width: 20px;
  font-size: 2rem;
  margin: .5rem;
  background-color: #EEE;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, .1);
}
.hits {
  font-size: 14px;
}
.number {
  max-width: max-content;
  margin: 0 auto .5rem auto;
}
.ok {
  color: yellowgreen;
}
.ko {
  color: tomato;
}
.title {
  font-size: .8rem;
  color: #AAA;
  font-weight: bold;
}
.title > span {
  font-size: 2rem;
  color: yellowgreen;
}
</style>
