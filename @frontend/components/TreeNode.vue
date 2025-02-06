<script setup lang="ts">

</script>

<template>
  <details class="treeNode">
    <summary>
      <slot name="title" />
    </summary>
    <div class="treeNode_details">
      <slot name="detail" />
    </div>
  </details>
</template>

<style scoped>
.treeNode {
  font-size: 1rem;
  cursor: pointer;
}

.treeNode_details {
  padding-left: 1rem;
}
</style>