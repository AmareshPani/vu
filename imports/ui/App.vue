<template>
<div class="app">
  <div v-blaze="'loginButtons'"></div>
  <p v-if="user">
    You are logged in as <b>{{ user.username }}</b>.
    <chat>:user="user.username"</chat>
  </p>
  <p v-else>
    Sign In to chat.
    
  </p>
</div>
</template>

<script>
import Chat from './Chat.vue';
import Test from './Test.vue';

import {Session} from 'meteor/session';

Session.setDefault("counter", 0);

let labels = ['Click me!', 'Click me again!', 'Here! Click here!', 'Again! Again!',
'Don\'t click me! No, I\'m just kidding. You can.', 'You like that?',
'Can you stratch me in the back please?', 'You are soooo nice! Click!',
'Hmmmm...', 'You know, you are wasting time clicking me.',
'No really, you can click me as much as you want.', 'Click me to level up!'];

export default {
  data() {
    return {
      buttonLabel: 'Click me!',
      count: 0,
      user: null,
    }
  },
  meteor: {
    data: {
      count () {
        return Session.get('counter');
      },
      user () {
        return Meteor.user()
      },
    }
  },
  methods: {
    addOne() {
      Session.set('counter', this.count + 1);
      this.buttonLabel = labels[Math.round(Math.random()*(labels.length - 1))];
    }
  },
  components: {
    Chat,
    Test,
  },
  metaInfo: {
    title: 'Meteor + Vue',
  },
};
</script>

<style>
body {
  margin: 30px;
}

a {
  color: #40b883;
  text-decoration: none;
}

h1, h2 {
  font-weight: normal;
}
</style>
