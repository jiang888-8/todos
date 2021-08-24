<template>
  <div class="todoapp">
    <todo-header @addTask='onadd' :arr='list'></todo-header>
    <todo-main :arr='cut' @del='del'></todo-main>
    <todo-footer :arr='list' :active='active' @deled='deled' @setActive='setActive'></todo-footer>
  </div>
</template>

<script>
import todoHeader from './components/todoHeader.vue'
import todoMain from './components/todoMain.vue'
import todoFooter from './components/todoFooter.vue'
export default {
  data () {
    return {
      list: JSON.parse(localStorage.getItem('listStr')) || [],
      active: 'all'
    }
  },

  components: {
    todoHeader,
    todoMain,
    todoFooter
  },

  watch: {
    list: {
      deep: true,
      handler () {
        localStorage.setItem('listStr', JSON.stringify(this.list))
      }
    }
  },

  computed: {
    cut () {
      if (this.active === 'undone') {
        return this.list.filter(item => {
          return !item.isDone
        })
      }
      if (this.active === 'done') {
        return this.list.filter(item => {
          return item.isDone
        })
      }
      return this.list
    }
  },

  methods: {
    onadd (val) {
      if (this.list.some(item => item.name === val)) return alert('任务已存在！')
      const id = this.list.length > 0 ? this.list[this.list.length - 1].id + 1 : 100
      this.list.push({
        id,
        name: val,
        isDone: false
      })
    },

    deled (val) {
      this.list = val
    },

    setActive (val) {
      this.active = val
    },

    del (id) {
      const index = this.list.findIndex(item => item.id === id)
      this.list.splice(index, 1)
    }
  }
}
</script>

<style scoped>

</style>
