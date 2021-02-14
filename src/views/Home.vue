<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>
    <Todos @badValue="triggerToast" />
  </div>
</template>

<script>
import { ref } from 'vue';
import Toast from '../components/Toast';
import Todos from '../components/Todos';

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false);

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => (showToast.value = false), 3000);
    };

    return { showToast, triggerToast };
  },
};
</script>

<style>
/* The enter-to and enter-from values become unnecessary due to the inclusion of the @keyframes
/* .toast-enter-from, */
.toast-leave-to {
  opacity: 0;
  transform: translateY(-60px);
}
/* .toast-enter-to, */
.toast-leave-from {
  opacity: 1;
  transform: translateY(0);
}
.toast-enter-active {
  /* transition: all 1s ease-in; */
  animation: wobble 1s ease;
}
.toast-leave-active {
  transition: all 1s ease-out;
}

@keyframes wobble {
  0% {
    transform: translateY(-60px);
    opacity: 0;
  }
  50% {
    transform: translateY(0px);
    opacity: 1;
  }
  60% {
    transform: translateX(8px);
  }
  70% {
    transform: translateX(-8px);
  }
  80% {
    transform: translateX(4px);
  }
  90% {
    transform: translateX(-4px);
  }
  100% {
    transform: translateX(0);
  }
}
</style>
