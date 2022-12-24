<template>
  <Container>
    <ChatWindow v-on:post-message="postMessage($event)">
      <ChatMessage 
      v-for="message in messageStore"
      v-bind:message="message"
      >
      </ChatMessage>
    </ChatWindow>
  </Container>
</template>
<script>
import Container from "./components/MyContainer.vue";
import ChatWindow from "./components/ChatWindow.vue";
import ChatMessage from "./components/ChatMessage.vue";

export default {
  name: "App",
  components: {
    Container, ChatMessage, ChatWindow,
  },
  data: () => ({
    messageStore:[],

  }),
  mounted(){
    this.getMessages()
  },
  methods:{
    async getMessages(){
      try{
        const response = await this.axios.get('https://61bcd385d8542f0017824a2a.mockapi.io/messages')
        this.messageStore = response.data
      }catch (e){
        alert(`error get ${e.data}`)
      }
    },
    async postMessage(message){
      try{
        await this.axios.post('https://61bcd385d8542f0017824a2a.mockapi.io/messages', message )
        this.getMessages()
      }catch(e){
        alert(`error post ${e.data}`)
      }
    }
  }

};
</script>
<style>
body {
  margin: 0;
  background-color: #f9f9fa;
}
</style>
