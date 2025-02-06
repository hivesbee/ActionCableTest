<script setup lang="ts">
import ActionCable from 'actioncable'

// 接続を生成（引数は、'ws://[Railsの接続URL]/cable'）
const cable = ActionCable.createConsumer('wss://localhost:3000/cable')

const chatChannel = cable.subscriptions.create(
  { channel: 'ChatChannel', room: 'チャットルーム' },
  {
    received({ type, body }) {
      switch (type) {
        case 'speak':
          messages.value.push(body)
          break
      }
    },
  }
)

const speak = () => {
  // performの第二引数でサーバー側の関数の引数を設定できる
  chatChannel.perform('speak', {
    message: input_message.value,
    name: name.value,
  })
  input_message.value = ''
}

const name = ref('')
const input_message = ref('')
const messages = ref([])
</script>

<template>
  <div>
    <!-- メッセージ一覧 -->
    <div v-for="message in messages">
      {{ message.name }}：{{ message.message }}
      <small>{{ message.spoke_at }}</small>
    </div>

    <!-- 入力 -->
    <h1>名前</h1>
    <input type="text" v-model="name" />
    <h1>内容</h1>
    <input type="text" v-model="input_message" />
    <button @click="speak">発言</button>
  </div>
</template>

<style scoped>

</style>