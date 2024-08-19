<template>
  <div class="chat-notice mt-10 ml-5 relative w-full" :class="fancy" :style="{
    transform: `rotate(${randomRotation()}deg)`
  }">
    <div class="header text-left px-5 py-1 absolute h-full w-full -top-8 -left-5 rounded-xl bg-purple-600 text-white">
      {{ username }}
    </div>
    <div class="message relative bg-white rounded-xl rounded-b-xl overflow-hidden py-3 px-5">
      <p class="text-gray-800 text-center font-bold">
        {{ username }} {{ message }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';
import Flower from "./Flares/flower.vue";
import EpicKitty from "./Badges/EpicKitty.vue";

const props = defineProps({
  username: {
    type: String,
    required: true
  },
  message: {
    type: String,
    required: true
  },
  tilt: {
    type: Boolean,
    required: false,
    default: true
  },
  fancy: {
    type: String,
    required: false,
    default: ''
  }
});

function randomRotation() {
  if (!props.tilt) return 0;
  return (Math.floor(Math.random() * 500) - 200) / 100;
}

</script>

<style scoped>
.chat-message:after {
  content: "";
  position: absolute;
  top: -2px;
  left: -2px;
  width: calc(100% + 4px);
  height: calc(100% + 4px);
  background-size: 400%;
  filter: blur(16px);
  border-radius: 0.75rem;
  opacity: 0.9;
  z-index: -2;
}

.chat-message:before {
  content: "";
  position: absolute;
  background: white;
  border-radius: 0.75rem;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: -1;
}

.sub:after {
  background: #A1ECD9;
}

.raid:after {
  background: #EEEB9F;
}

.cheer:after {
  background: #E89FEE;
}

@keyframes init {
  0%, 50% {
    top: -30px;
    left: -20px;
  }
  100% {
    top: 0;
    left: 0;
  }
}

.chat-notice .message {
  animation: init 1s ease;
  animation-iteration-count: 1;
}
</style>
