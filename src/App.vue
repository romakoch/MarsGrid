<template>
  <div id="app">
    <Nasa v-bind:numOfColAndRows="numOfColAndRows"></Nasa>
  </div>
</template>

<script>
import Nasa from "@/components/Nasa";

export default {
  name: 'App',
  data() {
	return {
		numOfColAndRows: [4,8]
	}
  },
  components: {
    Nasa,
  }
}
</script>

<style>

</style>
