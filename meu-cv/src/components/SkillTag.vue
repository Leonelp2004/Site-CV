<template>
  <span class="skill-tag">{{ name }}</span>
</template>

<script setup>
const props = defineProps({ name: String })
</script>

<style scoped>
.skill-tag {
  display: inline-block;
  background: #3498db;
  color: #fff;
  padding: 5px 12px;
  border-radius: 20px;
  margin: 5px;
  font-size: 0.9rem;
  transition: transform 0.2s, background 0.2s;
  cursor: default;
}
.skill-tag:hover {
  transform: scale(1.1);
  background: #2980b9;
}
</style>
