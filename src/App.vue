<template>
  <div class="container pr-1">
    <div class="card">
      <async-component></async-component>
    <h2>Динамические и асинхронные компоненты</h2>

      <app-button
          ref="myBtn"
          :color="oneColor"
          @action="active = 'one'"
      >One</app-button>
      <app-button
          :color="twoColor"
          @action="active = 'two'"
      >Two</app-button>
    </div>
    <keep-alive>
    <component :is="componentName"></component>
    </keep-alive>
  </div>
</template>

<script>
import AppButton from "@/components/AppButton"
import AppTextOne from "@/components/AppTextOne"
import AppTextTwo from "@/components/AppTextTwo"
// import AppAsyncComponent from "@/components/AppAsyncComponent"

export default {
  data() {
    return {
      active: 'one' // 'two'
    }
  },
  mounted() {
    /*setTimeout(() => {
      this.componentName = 'new comp name'
    }, 1500)*/
    this.$refs.myBtn.btnLog()
  },
  computed: {
    componentName: {
      get() {
        return 'app-text-' + this.active
      },
      set(value) {
        console.log('componentName', value)
      }
    },
    oneColor() {
      return this.active === 'one' ? 'primary' : ''
    },
    twoColor() {
      return this.active === 'two' ? 'primary' : ''
    }
  },
  components: {
    AppButton,
    AppTextOne,
    AppTextTwo,
    // AppAsyncComponent
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
