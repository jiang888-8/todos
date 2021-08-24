<template>
  <header class="header">
    <h1>todos</h1>
    <input v-model="isAll" id="toggle-all" class="toggle-all" type="checkbox" >
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model.trim="task"
      @keyup.enter="add"
    />
  </header>
</template>

<script>
export default {
  data () {
    return {
      task: ''
    }
  },

  props: ['arr'],

  computed: {
    isAll: {
      get () {
        return this.arr.every(item => item.isDone)
      },
      set (val) {
        this.arr.forEach(item => {
          item.isDone = val
        })
      }
    }
  },

  methods: {
    add () {
      if (!this.task) return alert('请输入任务名！')
      this.$emit('addTask', this.task)
      this.task = ''
    }
  }
}
</script>
