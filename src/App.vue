<template>
	<div class="vue-app" :id="app">
        <MainWrapper></MainWrapper>
    </div>
</template>

<script>
import MainWrapper from './views/MainWrapper.vue'

export default {
    data() {
        return {
            app: "app"
        };
    },
    components: { MainWrapper }
  }
</script>

<style>
.vue-app {    
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    flex-direction: column;
}

</style>