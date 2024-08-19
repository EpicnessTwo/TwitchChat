<template>
  <div class="chat-message mt-12 ml-5 relative" :class="{
    'rainbow': messageFlare === 'rainbow',
    'w-full': !isSingleEmote,
    'text-center': isSingleEmote,
  }" :style="{
    transform: `rotate(${randomRotation()}deg)`
  }">
    <div class="header text-left px-5 py-1 absolute h-full w-full -top-8 -left-5 rounded-xl" :class="messageAccent">
      <div class="catear_left" :class="messageAccent"></div>
      <div class="catear_right" :class="messageAccent"></div>
        <span class="font-medium">{{ username }}</span>
        <span v-if="props.pronouns.pronouns" class="text-xs">
          ({{ props.pronouns.pronouns }})
        </span>
    </div>
    <div
        class="message relative bg-white rounded-xl rounded-b-xl overflow-hidden"
        :class="{
          'py-3 px-5': !isSingleEmote,
          'text-center': isSingleEmote,
        }"
    >
        <EmoteSpam v-if="props.tags['animation-id'] === 'simmer'"></EmoteSpam>
        <template v-if="isSingleEmote">
          <component :is="Emote" :id="parsedMessage[0].id" :alt="parsedMessage[0].alt" :emote-source="parsedMessage[0].emoteSource" class="!h-32 !min-w-32 w-auto"></component>
        </template>
        <template v-else>
          <span v-for="part in parsedMessage" :key="part.key">
            <component v-if="part.type === 'emote'" :is="Emote" :id="part.id" :alt="part.alt" :emote-source="part.emoteSource"></component>
            <span v-else>{{ part.text }}</span>
            <span class="inline-block w-1"> </span>
          </span>
        </template>
    </div>
  </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';
import Flower from "./Flares/flower.vue";
import Emote from "./Emote.vue";
import Mod from "./Badges/Mod.vue";
import Sub from "./Badges/Sub.vue";
import Vip from "./Badges/Vip.vue";
import Host from "./Badges/Host.vue";
import EpicKitty from "./Badges/EpicKitty.vue";
import FlowerLeft from "./Flares/FlowerLeft.vue";
import EmoteSpam from "./Flares/EmoteSpam.vue";

const props = defineProps({
  username: {
    type: String,
    required: true
  },
  message: {
    type: String,
    required: true
  },
  tags: {
    type: Object,
    required: true
  },
  tilt: {
    type: Boolean,
    required: false,
    default: true
  },
  stvEmotes: {
    type: Object,
    required: false,
    default: () => ({})
  },
  pronouns: {
    type: [Object, Boolean],
    required: false,
    default: false
  }
});

// Calculate the luminance of props.tags.color to determine text colour, setting a var called textColour
let textColour = 'text-white';
if (props.tags.color) {
  const hex = props.tags.color.replace('#', '');
  textColour = ((0.299 * parseInt(hex.substring(0, 2), 16) + 0.587 * parseInt(hex.substring(2, 4), 16) + 0.114 * parseInt(hex.substring(4, 6), 16)) / 255) > 0.5 ? 'text-black' : 'text-white';
}


let messageAccent = 'bg-[' + ((props.tags.color === '#FFFFFF' ? '#D946EF' : props.tags.color) ?? '#D946EF') + '] ' + textColour;
let messageFlare = '';
let isEpicKitty = false;

if (props.tags['display-name'] === 'EpicKittyXP') {
  isEpicKitty = true;
}

// Animations
if (props.tags['animation-id'] === 'rainbow-eclipse') {
  messageFlare = 'rainbow';
}

const parsedMessage = computed(() => parseMessage(props.message, props.tags.emotes));
const isSingleEmote = computed(() => parsedMessage.value.length === 1 && parsedMessage.value[0].type === 'emote');

function parseMessage(message, emotes) {
  let response = message;

  response = parseMessageTwitch(response, emotes); // Parse Twitch emotes
  response = parseMessage7tv(response, props.stvEmotes); // Parse 7TV emotes

  return response;
}

function parseMessageTwitch(message, emotes) {
  if (!emotes) {
    return message.split(/\s+/).map((word, index) => ({
      type: 'text',
      text: word,
      key: `text-${index}`
    }));
  }

  const emotePositions = [];
  for (const emoteId in emotes) {
    const positions = emotes[emoteId];
    positions.forEach(position => {
      const [start, end] = position.split('-').map(Number);
      emotePositions.push({ start, end, id: emoteId });
    });
  }

  emotePositions.sort((a, b) => a.start - b.start);

  const parsed = [];
  let lastIndex = 0;
  emotePositions.forEach(({ start, end, id }, index) => {
    if (start > lastIndex) {
      const textPart = message.substring(lastIndex, start);
      textPart.split(/\s+/).forEach((word, wordIndex) => {
        if (word) {
          parsed.push({
            type: 'text',
            text: word,
            key: `text-${lastIndex + wordIndex}`
          });
        }
      });
    }
    parsed.push({
      type: 'emote',
      emoteSource: 'twitch',
      id,
      alt: message.substring(start, end + 1),
      key: `emote-${index}`
    });
    lastIndex = end + 1;
  });

  if (lastIndex < message.length) {
    const textPart = message.substring(lastIndex);
    textPart.split(/\s+/).forEach((word, wordIndex) => {
      if (word) {
        parsed.push({
          type: 'text',
          text: word,
          key: `text-${lastIndex + wordIndex}`
        });
      }
    });
  }

  return parsed;
}

function parseMessage7tv(message, emotes) {
  const parsed = [];

  message.forEach((part) => {
    if (part.type === 'text') {
      if (emotes[part.text]) {
        parsed.push({
          type: 'emote',
          emoteSource: '7tv',
          id: emotes[part.text].id,
          alt: part.text
        });
      } else {
        parsed.push(part);
      }
    } else {
      parsed.push(part);
    }
  });

  return parsed;
}

function randomRotation() {
  if (!props.tilt) return 0;
  return (Math.floor(Math.random() * 500) - 200) / 100;
}

</script>
<style scoped>
.rainbow:after {
  content: "";
  position: absolute;
  top: -10px;
  left: -10px;
  width: calc(100% + 20px);
  height: calc(100% + 20px);
  background: linear-gradient(45deg, #fb0094, #0000ff, #00ff00, #ffff00, #ff0000, #fb0094, #0000ff, #00ff00, #ffff00, #ff0000);
  background-size: 400%;
  animation: rainbow 20s linear infinite;
  filter: blur(16px);
  border-radius: 0.75rem;
  opacity: 0.9;
  z-index: -2;
}

.rainbow:before {
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

@keyframes rainbow {
  0% {
    background-position: 0 0;
  }
  50.01% {
    background-position: 200% 0;
  }
  100% {
    background-position: 0 0;
  }
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

.chat-message .message {
  animation: init 1s ease;
  animation-iteration-count: 1;
}

/*
.catear_left,
.catear_right {
  content: "";
  position: absolute;
  display: block;
  width: 40px;
  height: 100px;
  z-index: -1;
  border-radius: 100%;
  top: -20px;
}

.catear_left {
  left: 15px;
}

.catear_right {
  right: 15px;
}*/
</style>
