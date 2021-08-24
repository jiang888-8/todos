<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>{{residue}}</strong></span>
    <ul class="filters">
      <li>
        <a :class="{selected: active === 'all'}" href="javascript:;" @click="$emit('setActive', 'all')">全部</a>
      </li>
      <li>
        <a :class="{selected: active === 'undone'}" href="javascript:;" @click="$emit('setActive', 'undone')">未完成</a>
      </li>
      <li>
        <a :class="{selected: active === 'done'}" href="javascript:;" @click="$emit('setActive', 'done')">已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="del">清除已完成</button>
  </footer>
</template>

<script>
export default {
  data () {
    return {
      done: []
    }
  },

  props: ['arr', 'active'],

  computed: {
    residue () {
      return this.arr.filter(item => !item.isDone).length
    }
  },

  methods: {
    del () {
      const done = this.arr.filter(item => {
        return !item.isDone
      })
      this.$emit('deled', done)
    }
  }
}
</script>
