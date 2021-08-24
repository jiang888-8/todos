<template>
  <div class="todoapp">
    <todo-header></todo-header>
    <todo-main></todo-main>
    <todo-footer/>
  </div>
</template>

<script>
import todoHeader from './components/todoHeader.vue'
import todoMain from './components/todoMain.vue'
import todoFooter from './components/todoFooter.vue'
export default {
  data () {
    return {

    }
  },

  components: {
    todoHeader,
    todoMain,
    todoFooter
  },

  created () {

  },

  methods: {

  }
}
</script>

<style scoped>

</style>
