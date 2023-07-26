<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
    <button @click="addTodo">add</button>
    <span class="addContainer">
      <i class="fas fa-plus addBtn"></i>
    </span>
    <CommonModal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고!
        <span @click="showModal = false">닫기</span>
      </h3>
      sdfsdfsd
      <p slot="body">무언가를 입력하세요.</p>
      <footer slot="footer">copylight</footer>
    </CommonModal>
  </div>
</template>

<script>
import CommonModal from './common/CommonModal.vue';
export default {
  data() {
    return {
      newTodoItem: '',
      showModal: false,
  }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        // this.$emit('addTodoItem', this.newTodoItem)
        this.$store.commit('addOneItem', this.newTodoItem);
      } else {
        this.showModal = !this.showModal
      }
      this.clearInput();
    },
    clearInput() {
    this.newTodoItem = ''
    }
  },
  components: {
    CommonModal,
  },
  created() {
    for (let i = 0; i < localStorage.length; i++) {
      this.todoList.unshift(JSON.parse(localStorage.getItem(localStorage.key(i))))
    }
}
}
</script>

<style scoped>
input:foces {
  outline: none;
}

.inputBox {
  background-color: #fff;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}

.inputBox inpur {
  border-style: none;
  font-size: 0.9rem;
}
</style>