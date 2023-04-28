<script lang="ts">
import { defineComponent, ref } from 'vue'
interface Joke {
  joke: string
}
export default defineComponent({
  name: 'Chuck-Norris-Jokes',
  setup() {
    const name = ref<string>('')
    const joke = ref<Joke>('')

    const getJoke = async () => {
      try {
        const response = await fetch(`https://api.chucknorris.io/jokes/random?name=${name.value}`)
        const data = await response.json()
        joke.value = data.value
      } catch (error) {
        console.error(error)
      }
    }
    return { name, joke, getJoke }
  }
})
</script>
<template>
  <div class="container">
    <form class="form" @submit.prevent="getJoke">
      <div id="button-wrapper">
        <h1 class="title">Type a name to get a Chuck Norries Joke!</h1>
        <input type="text" placeholder="Enter a name" v-model="name" />
        <button class="" type="submit" :disabled="!name">Get Joke</button>
      </div>
    </form>
    <div id="joke" v-if="joke">{{ joke }}</div>
  </div>
</template>
<style scoped>
.container {
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  grid-template-rows: repeat(10, 1fr);
  height: 100vh;
  background: #a9b4c2;
  border: 10px solid rgb(103, 67, 67);
  place-items: center;
}

.form {
  grid-column: 4 / 8;
  grid-row: 4 / 8;
  display: flex;
  justify-content: center;
  align-items: center;
}
#button-wrapper {
  display: flex;
  align-items: center;
  flex-direction: column;
}
.title {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  text-align: center;
}
#joke {
  grid-column: 3 / span 6;
  grid-row: 5 / span 6;
  display: flex;
  justify-content: center;
  align-items: center;
}

input,
button {
  height: 2rem;
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
}

input {
  flex: 1;
  margin-right: 0.5rem;
  border: 2px solid #cdcbef;
}

button {
  background-color: #8000ff;
  color: #fff;
  border: none;
  border-radius: 0.25rem;
  cursor: pointer;
  margin: 1em;
}
</style>
