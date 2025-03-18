<template>
    <div>
      <button class="chat-icon" @click="toggleChat">💬</button>
      <div v-if="isOpen" class="chat-container">
        <div class="chat-header">
          <span>Lilly - Your Assistant</span>
          <button class="close-btn" @click="toggleChat">&times;</button>
        </div>
        <div class="chat-box" ref="chatBox">
          <div v-if="history.length === 0" class="welcome-message">Hello! How can I help you?</div>
          <div v-for="(message, index) in history" :key="index" :class="['message', message.role]">
            <img :src="message.role === 'user' ? userAvatar : botAvatar" class="avatar" />
            <div class="message-content">
              <strong v-if="message.role === 'user'">You: </strong>
              <strong v-else>Lilly: </strong>
              <span>{{ message.content }}</span>
            </div>
          </div>
          <div v-if="isTyping" class="typing">Lilly is typing...</div>
        </div>
        <div class="input-area">
          <input v-model="userMessage" @keyup.enter="sendMessage" placeholder="Type a message..." ref="messageInput" />
          <button @click="sendMessage">Send</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        userMessage: '',
        history: [
          { role: 'assistant', content: "Hello! My name is Lilly, and I was created and trained by Abhay. How can I assist you today?" }
        ],
        isOpen: false,
        isTyping: false,
        userAvatar: 'https://i.pravatar.cc/40?img=3', // Placeholder user avatar
        botAvatar: 'https://i.pravatar.cc/40?img=5' // Placeholder bot avatar
      };
    },
    methods: {
      toggleChat() {
        this.isOpen = !this.isOpen;
      },
      async sendMessage() {
        if (!this.userMessage.trim()) return;
  
        this.history.push({ role: 'user', content: this.userMessage });
        this.isTyping = true;
        this.$nextTick(() => this.scrollToBottom());
        
        const userInput = `Answer concisely: ${this.userMessage}`;
        this.userMessage = ''; // Clear input instantly
        
        const queryParams = new URLSearchParams({
          chat: userInput,
          history: encodeURIComponent(JSON.stringify(this.history))
        });
  
        try {
          const response = await fetch(`https://simple-chats.abhay007official.workers.dev/?${queryParams.toString()}`);
          const data = await response.json();
          let botResponse = data.response.response;
  
          setTimeout(() => {
            this.history.push({ role: 'assistant', content: botResponse });
            this.isTyping = false;
            this.$nextTick(() => this.scrollToBottom());
          }, 1000);
        } catch (error) {
          console.error('Error fetching response:', error);
          this.isTyping = false;
        }
      },
      scrollToBottom() {
        this.$nextTick(() => {
          if (this.$refs.chatBox) {
            this.$refs.chatBox.scrollTop = this.$refs.chatBox.scrollHeight;
          }
        });
      }
    }
  };
  </script>
  
  <style>
  .chat-icon {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: #474ce6;
    color: white;
    border: none;
    border-radius: 50%;
    width: 55px;
    height: 50px;
    font-size: 24px;
    cursor: pointer;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
  }
  .chat-container {
    position: fixed;
    bottom: 80px;
    right: 20px;
    width: 320px;
    background: white;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    display: flex;
    flex-direction: column;
  }
  .chat-header {
    background: #474ce6;
    color: white;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
  }
  .close-btn {
    background: none;
    border: none;
    font-size: 18px;
    cursor: pointer;
    color: white;
  }
  .chat-box {
    height: 300px;
    overflow-y: auto;
    padding: 10px;
    display: flex;
    flex-direction: column;
  }
  .welcome-message {
    text-align: center;
    color: gray;
    margin-bottom: 10px;
  }
  .message {
    display: flex;
    align-items: center;
    margin: 10px 0;
  }
  .avatar {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    margin-right: 10px;
  }
  .message-content {
    background: #f1f1f1;
    padding: 8px;
    border-radius: 10px;
    max-width: 75%;
  }
  .user .message-content {
    background: #474ce6;
    color: white;
    align-self: flex-end;
  }
  .input-area {
    display: flex;
    padding: 10px;
    border-top: 1px solid #ccc;
    background: #f9f9f9;
  }
  input {
    flex: 1;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  button {
    background: #474ce6;
    color: white;
    border: none;
    padding: 8px 12px;
    margin-left: 5px;
    border-radius: 5px;
    cursor: pointer;
  }
  .typing {
    font-size: 14px;
    color: gray;
    padding-left: 10px;
  }
  </style>
  
