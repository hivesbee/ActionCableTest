<script setup lang="ts">
const props = defineProps<{
  nodes: any
}>()

const emit = defineEmits<{
  nodeClick: [node: any]
  treeClick: [node: any]
}>()

const nodeClick = (node: any) => {
  treeClick(node)
}

const treeClick = (node: any) => {
  emit('treeClick', node)
}

</script>

<template>
  <template v-for="node in props.nodes">
    <tree-node @click.stop="nodeClick(node)">
      <template #title>
        {{ node.title }}
      </template>
      <template #detail>
        {{ node.detail }}
        <template v-if="node.children">
          <tree :nodes="node.children" @treeClick="treeClick" />
        </template>
      </template>
    </tree-node>
  </template>
</template>

<style scoped>

</style>