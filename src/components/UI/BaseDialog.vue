<template>
  <Teleport to="body">
    <div @click="$emit('close')" class="overlay"></div>
    <dialog open>
      <div class="header">
        <slot name="header">
          <h2>{{ title }}</h2>
        </slot>
      </div>
      <div class="content">
        <slot></slot>
      </div>
      <div class="menu">
        <slot name="actions">
          <BaseButton @click="$emit('close')">Close</BaseButton>
        </slot>
      </div>
    </dialog>
  </Teleport>
</template>

<script>
import { Teleport } from 'vue';

export default {
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  emits: ['close'],
  components: { Teleport },
};
</script>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 10;
}

dialog {
  position: fixed;
  top: 20vh;
  left: 10%;
  width: 80%;
  z-index: 100;
  border-radius: 12px;
  border: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0;
  margin: 0;
  overflow: hidden;
}

.header {
  background-color: #3a0061;
  color: white;
  width: 100%;
  padding: 1rem;
}

.header h2 {
  margin: 0;
}

.content {
  padding: 1rem;
}

.menu {
  padding: 1rem;
  display: flex;
  justify-content: flex-end;
  margin: 0;
}

@media (min-width: 768px) {
  dialog {
    left: calc(50% - 20rem);
    width: 40rem;
  }
}
</style>
