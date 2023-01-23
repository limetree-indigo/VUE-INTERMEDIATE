<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
    <span class="addContainer" @click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
    <Teleport to="body">
      <!-- use the modal component, pass in the prop -->
      <ModalComponent :show="showModal" @close="showModal = false">
        <template #header>
          <h3>경고!
            <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
          </h3>
        </template>
        <template #body>
          <div>
            아무것도 입력하지 않았습니다.
          </div>
        </template>
        templ
      </ModalComponent>
    </Teleport>
  </div>
</template>
<script>
import ModalComponent from './common/ModalComponent.vue'

export default {
  components: {
    ModalComponent
  },
  data () {
    return {
      newTodoItem: '',
      showModal: false
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoItem !== '') {
        this.$emit('addTodoItem', this.newTodoItem)
        this.clearInput()
      } else {
        this.showModal = !this.showModal
      }
    },
    clearInput: function () {
      this.newTodoItem = ''
    }
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478fb, #8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}
.addBtn {
  color: white;
  vertical-align: middle;
}
.closeModalBtn {
  color: #42b983;
}
</style>
