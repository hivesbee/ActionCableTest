<script setup lang="ts">
import { v4 as uuidv4 } from 'uuid'

const initNode = [
  {
    id: uuidv4(),
    title: 'title',
    detail: 'detail',
    children: [
      {
        id: uuidv4(),
        title: 'child',
        detail: 'child detail',
        children: []
      }
    ]
  }
]

const nodes = ref<any>(initNode)

const title = ref<string>('')
const detail = ref<string>('')

const addNode = () => {
  if (title.value === '') {
    return
  }

  nodes.value.push({
    id: uuidv4(),
    title: title.value,
    detail: detail.value,
    children: [],
  })

  title.value = ''
  detail.value = ''
}

const currentNode = ref<any>({})

const nodeClick = (node: any) => {
  console.log(node)
  currentNode.value = node
}
</script>

<template>
  <div>
    <p>
      選択中のノード : {{ currentNode.id }}
    </p>
    <input type="text" placeholder="選択中のタイトル" v-model="currentNode.title">
    <input type="text" placeholder="選択中の詳細" v-model="currentNode.detail">

  </div>
  <hr />
  <div>
    <input type="text" placeholder="タイトル" v-model="title">
    <input type="text" placeholder="詳細" v-model="detail">
    <button type="button" @click="addNode">
      ノード追加
    </button>
  </div>
  <hr />

  <tree :nodes="nodes" @treeClick="nodeClick" />

  <tree-node>
    <template #title>
      hoge
    </template>
    <template #detail>
      aaaa
      <tree-node>
        <template #title>
          fuga
        </template>
        <template #detail>
          bbbbb
        </template>
      </tree-node>
    </template>
  </tree-node>
</template>

<style scoped>

</style>