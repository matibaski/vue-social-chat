<template>
  <div>
    <hr>
    <h1>Custom form in popup</h1>
    <h2>Example: Newsletter form</h2>
    <SocialChat
      icon
      @close="resetForm"
    >
      <template v-slot:header>
        <p>Subscribe to our newsletter and know everything about anything</p>
      </template>
      <template v-slot:body>
        <div
          v-show="!subscribed"
          class="newsletter"
        >
          <label for="name">
            <span>Name</span>
            <input
              v-model="newsletter.name"
              name="name"
              type="text"
              aria-label="Type your name"
            >
          </label>
          <label for="email">
            <span>Email</span>
            <input
              v-model="newsletter.email"
              name="email"
              type="email"
              aria-label="Type your email"
            >
          </label>
          <button
            type="button"
            aria-label="Confirm subscribe"
            @click="send"
          >
            SUBSCRIBE
          </button>
        </div>
        <strong v-show="subscribed">Successfully subscribed</strong>
      </template>
      <template v-slot:button="{ open }">
        <img
          v-show="!open"
          src="https://raw.githubusercontent.com/ktquez/vue-social-chat/master/src/icons/email.svg"
          alt="icon email"
          aria-hidden="true"
        >
        <span v-show="open">CLOSE</span>
      </template>
    </SocialChat>
  </div>
</template>

<script>
import { SocialChat } from '../../vue-social-chat'

export default {
  name: 'WhatsAppPage',

  components: {
    SocialChat
  },

  data: () => ({
    newsletter: {
      name: '',
      email: ''
    },
    subscribed: false
  }),

  methods: {
    send () {
      this.subscribed = true
    },

    resetForm () {
      setTimeout(() => {
        this.newsletter = { name: '', email: '' }
        this.subscribed = false
      }, 500)
    }
  }
}
</script>

<style>
.newsletter {
  display: flex;
  flex-wrap: wrap;
}

.newsletter label {
  width: 100%;
  margin-bottom: 20px;
}

.newsletter label > input {
  padding: 10px;
  width: 100%;
  margin-top: 4px;
}

.newsletter button {
  padding: 14px;
  background-color: #333;
  border:none;
  color: white;
  border-radius: 30px;
  cursor: pointer;
  margin-bottom: 8px;
}
</style>
