<template>
  <div class="q-pa-md q-gutter-sm">
    <q-btn label="Remove and restore children" @click="refreshChildren" />
    <q-tree
      v-model:expanded="expanded"
      v-model:selected="selected"
      :nodes="nodes"
      node-key="id"
    />
    <div>Selected: {{ selected || 'none' }}</div>
  </div>
</template>

<script setup>
import { nextTick, ref } from 'vue'

const originalNodes = [
  {
    id: 'root',
    label: 'Root',
    children: [{ id: 'child', label: 'Child' }]
  }
]
const nodes = ref(originalNodes)
const expanded = ref(['root'])
const selected = ref(null)

function refreshChildren() {
  nodes.value = [{ id: 'root', label: 'Root', children: [] }]
  nextTick(() => {
    nodes.value = originalNodes
  })
}
</script>
