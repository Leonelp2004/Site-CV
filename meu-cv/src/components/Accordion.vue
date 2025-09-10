<template>
  <div class="accordion-container">
    <button class="accordion-btn" @click="toggle">
      {{ title }}
      <span class="arrow" :class="{ open: open }">▼</span>
    </button>
    <transition name="slide">
      <div class="accordion-panel" v-show="open">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, watchEffect } from 'vue'
const props = defineProps({
  title: String,
  defaultOpen: { type: Boolean, default: false }  
})

const open = ref(props.defaultOpen)
const toggle = () => (open.value = !open.value)
</script>

<style scoped>
.accordion-btn {
  width: 100%;
  background: #5a4bdc;
  color: #fff;
  padding: 15px;
  border: none;
  border-radius: 8px;
  font-size: 1.1rem;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: background 0.3s;
}
.accordion-btn:hover { background: #5a4bdc; }
.arrow { transition: transform 0.3s; }
.arrow.open { transform: rotate(180deg); }

.accordion-panel {
  background: #fff;
  padding: 15px;
  border-radius: 0 0 8px 8px;
  margin-bottom: 15px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

/* Transição */
.slide-enter-active, .slide-leave-active { transition: all 0.3s ease; }
.slide-enter-from, .slide-leave-to { max-height: 0; opacity: 0; padding: 0 15px; }
.slide-enter-to, .slide-leave-from { max-height: 500px; opacity: 1; }
</style>
