<template>
  <div class="chat">
    <h2>Chat</h2>

    <input v-model="newMessage" @keyup.enter="sendMessage" placeholder="Enter new message" />
    
    <div v-if="!$subReady.messages">
      Loading...
    </div>

    <div class="collection">
     <a href="#!" class="collection-item" v-for="msg in messages">
      <span>
      <button class="btn" @click="removeMessage(msg._id)">x</button></span>
      {{ msg.message }}</a> 
    </div>
  </div>
</template>

<script>
const test = {
  meteor: {
    subscribe: {
      'messages': [],
    },
    messages() {
      return Messages.find({}, {
        sort: { },
      }).fetch().reverse();
    },
  },
}

export default {
  name: 'chat',
  mixins: [test],
  data () {
    return {
      newMessage: '',
      messages: [],
    }
  },
  props: {
   user : String
  },
  meteor: {
    messages() {
      return Messages.find({}, {
        sort: { date: 1 },
      }).fetch().reverse();
    },
  },
  methods: {
    sendMessage() {
      var msg = Meteor.user().username + ': ' + this.newMessage;
      Meteor.call('addMessage', msg);
      this.newMessage = '';
      
    },
    getUser(){     
     return Meteor.user().username;
    },
    removeMessage(_id) {
      Meteor.call('removeMessage', _id);
    },
  },
};
</script>

<style scoped>
.chat {
  max-width: 300px;
}

input {
  width: 100%;
  box-sizing: border-box;
  padding: 6px 12px;
  border: solid 1px #ccc;
  border-radius: 3px;
  margin-bottom: 4px;
}

.message {
  margin: 4px 2px;
  display: flex;
  flex-direction: row;
}

.message .content {
  flex: auto 1 1;
}
</style>
