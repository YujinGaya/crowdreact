<template>
  <div class="emotion-comment">
    <div class="field">
      <p class="control">
        <input v-model="message"
          ref="input"
          class="input is-rounded"
          placeholder="What's happening?">
        <span @click="send"
          class="send-button-container">
          <i class="fas fa-paper-plane"></i>
        </span>
      </p>
    </div>
    <transition
      @before-enter="beforeEnter"
      @after-enter="afterEnter">
      <div
        v-show="sending"
        class="plane">
        <!-- {{ message }} -->
        <i class="fas fa-paper-plane"></i>
      </div>
    </transition>
  </div>
</template>

<script>
import { sendComment } from '@/firebase/emotion.js'

export default {
  data () {
    return {
      sending: false,
      message: ''
    }
  },
  methods: {
    send () {
      this.$ga.event('Comment', 'Sent', this.message)
      sendComment(this.message)
      this.sending = true
      this.message = ' '
      setTimeout(() => {
        this.sending = false
        this.message = ''
      }, 500)
    },
    beforeEnter (el) {
      const { top, left } = this.$refs.input.getBoundingClientRect()

      el.style.top = top + window.scrollY + 3 + 'px'
      el.style.left = left + 4 + 'px'
      el.style.fontSize = '1rem'
    },
    afterEnter (el) {
      el.style.top = '1rem'
      el.style.left = 'calc(100% - 2rem)'
      el.style.fontSize = '0.5rem'
    }
  }
}
</script>

<style scoped>
.emotion-comment input {
  border: 1px solid #dbdbdb;
  border-radius: 1rem;
  box-shadow: none;
  transition: all 0.2s ease;
}

.emotion-comment input:focus {
  border: 1px solid #ababab;
}

.field {
  margin-bottom: 0;
}

.control {
  position: relative;
}

.send-button-container {
  position: absolute;
  top: 0rem;
  right: 0rem;
  padding: 0.2rem 0.5rem 0.2rem 0.4rem;
  margin: 0.175rem;
  border-radius: 1rem;
  background-color: var(--theme-blue);

  cursor: pointer;
}

.plane {
  position: absolute;
  padding: 0.2em 0.5em 0.2em 0.4em;
  border-radius: 1rem;
  background-color: var(--theme-blue);
  white-space: nowrap;
  transition:
    top 0.4s ease-out,
    left 0.4s ease-in,
    font-size 0.4s ease-in;
}
</style>
