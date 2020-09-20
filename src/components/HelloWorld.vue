<template>
  <button @click="showToast" class="btn">打开 toast</button>
  <!-- to 属性就是目标位置 -->
  <teleport to="#teleport-target">
    <div v-if="visible" class="toast-wrap">
      <div class="toast-msg">我是一个 Toast 文案</div>
    </div>
  </teleport>

  <button id="show-modal" class="btn" @click="showModal = true">展示 Modal</button>
  <teleport to="#modal-container">
    <!-- use the modal component, pass in the prop -->
    <modal :show="showModal" @close="showModal = false">
      <template #header>
        <h3>custom header</h3>
      </template>
    </modal>
  </teleport>
</template>

<script>
import { ref } from 'vue';
import Modal from './Modal.vue';

export default {
  name: 'HelloWorld',
  components: {
    Modal
  },
  setup() {
    // toast 的封装
    const visible = ref(false);
    let timer;
    const showToast = () => {
      visible.value = true;
      clearTimeout(timer);
      timer = setTimeout(() => {
        visible.value = false;
      }, 2000);
    }

    // modal 的封装
    const showModal = ref(false);

    return {
      visible,
      showToast,
      showModal
    }
  }
}
</script>

<style>
.btn {
  background: linear-gradient(rgba(27,188,194,1) 0%, rgba(24,163,168,1) 100%);
  padding: 4px 12px;
  font-size: 12px;
  text-decoration: none;
  color: white;
  padding: 10px 30px;
  display: inline-block;
  position: relative;
  border: 1px solid rgba(0,0,0,0.21);
  border-bottom: 4px solid rgba(0,0,0,0.21);
  border-radius: 4px;
  text-shadow: 0 1px 0 rgba(0,0,0,0.15);
  margin: 10px;
}
 .toast-wrap {
  opacity: 1;
  top: 20%;
  color: #fff;
  width: 30%;
  margin: 0 auto;
  text-align: center;
}
.toast-msg {
  background-color: rgba(0,0,0,0.7);
  padding: 2px 5px;
  border-radius: 5px;
}
</style>
