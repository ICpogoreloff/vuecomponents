<template>
  <div class="container pr-1">
    <div class="card">
    <h2>Динамические и синхронные компоненты</h2>

      <app-button
          :color="active === 'one' ? 'primary' : ''"
          @action="active = 'one'"
      >One</app-button>
      <app-button
          :color="active === 'two' ? 'primary' : ''"
          @action="active = 'two'"
      >Two</app-button>
    </div>

    <component :is="componentName"></component>
  </div>
</template>

<script>
import AppButton from "@/components/AppButton"
import AppTextOne from "@/components/AppTextOne"
import AppTextTwo from "@/components/AppTextTwo"

export default {
  data() {
    return {
      active: 'one' // 'two'
    }
  },
  computed: {
    componentName() {
      return 'app-text-' + this.active
    }
  },
  components: {
    AppButton,
    AppTextOne,
    AppTextTwo
  }
}
</script>

<style scoped>

app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
