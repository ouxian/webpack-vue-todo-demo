<template>
  <div :class="['todo-item', todo.completed ? 'completed' : '']">
    <input 
      type="checkbox"
      class="toggle"
      v-model="todo.completed"
    >
    <label>{{todo.content}}</label>
    <button class="destory" @click="deleteTodo"></button>
  </div>
</template>

<script>
export default {
  props: {  //item是子组件，todo是父组件。被引用的就是子组件。如A引用B，则A就是父组件，B就是子组件
    todo: {  //子组件在prop里面声明一个变量(这里是todo)，这个变量就可以引用父元素的数据(各种数据)，在父组件中通过:todo="todo"传过来
      type: Object,
      required: true,
    }
  },
  methods: {
    deleteTodo() {
      this.$emit('del', this.todo.id)   //子组件调用父组件的方法并传递数据(参数)，比如这里是调用父组件的‘del’方法，并传递参数'this.todo.id'给父组件
    }
  }
}
</script>

<style lang="stylus" scoped>
.todo-item{
  position relative
  background-color #fff
  font-size 24px
  border-bottom 1px solid rgba(0,0,0,0.06)
  &:hover{
    .destory:after{
      content: '×'
    }
  }
  label{
    white-space: pre-line;
    word-break: break-all;
    padding: 15px 60px 15px 15px;
    margin-left: 45px;
    display: block;
    line-height: 1.2;
    transition: color 0.4s;
  }
  &.completed{
    label{
      color: #d9d9d9;
      text-decoration line-through
    }
  }
}
.toggle{
  text-align: center;
  width: 40px;
  height: 40px;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto 0;
  border: none;
  appearance: none;
  outline none
  &:after{
    content url('../assets/images/round.svg')
  }
  &:checked:after{
    content url('../assets/images/done.svg')
  }
}
.destory{
  position: absolute;
  top: 0;
  right: 10px;
  bottom: 0;
  width: 40px;
  height: 40px;
  margin: auto 0;
  font-size: 30px;
  color: #cc9a9a;
  margin-bottom: 11px;
  transition: color 0.2s ease-out;
  background-color transparent
  appearance none
  border-width 0
  cursor pointer
  outline none
}
</style>


