<template>
  <div id="app">
    <div
      v-for="country in countries"
      :key="country.key"
      class="country"
    >
      <h1>{{country.key}}</h1>
      <hr />
      <h2>{{country.sources.domestic[0]}}</h2>
    </div>
  </div>
</template>

<script lang="ts">
import { Vue } from 'vue-property-decorator'

export default class App extends Vue {
  get countries () {
    const requireContext = require.context(
      './constants/countries',
      true,
      /(.*)\.yml/
    )
    return requireContext.keys().map((fileName) => {
      const key: string = fileName.split('.')[1].replace('/', '')
      return {
        key: key,
        ...requireContext(fileName)[key]
      }
    })
  }
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
.country{
  border:1px solid black;
  margin:20px;
}
</style>
