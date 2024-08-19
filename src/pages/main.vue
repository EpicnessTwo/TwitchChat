<template>
  <div class="flex flex-wrap max-w-full max-h-screen z-10 relative">
    <div class="flex-1 m-4">
      <div class="w-full aspect-[16/9] block bg-green-500 rounded-xl mb-4"></div>
      <div class="grid grid-cols-3 grid-rows-2 gap-4 h-[12.2rem]">
        <div class="row-start-1 rounded-xl font-bold">
          <svg xmlns="http://www.w3.org/2000/svg" version="1.1" xmlns:xlink="http://www.w3.org/1999/xlink" width="100%" height="100%">
            <!-- Background -->
            <rect x="0" y="0" fill="transparent" width="100%" height="100%" />
            <!-- Text using the #pattern in defs as the fill -->
            <text x="45%" text-anchor="middle" y="50%" dy="0.4em" fill="url(#pattern)"  font-size="80px">EpicKittyXP</text>
            <defs>
              <!-- Da gradient -->
              <linearGradient id="gradient" x1="0%" y1="40%" x2="100%" y2="0">
                <stop offset="0%" style="stop-color:#8BD3E6;" />
                <stop offset="25%" style="stop-color:#FF6D6A;" />
                <stop offset="50%" style="stop-color:#E9EC6B;" />
                <stop offset="75%" style="stop-color:#EFBE7D;" />
                <stop offset="100%" style="stop-color:#B1A2CA;" />
              </linearGradient>
              <!-- Stitch 2 gradients together for seamless animation  -->
              <pattern id="pattern" x="0" y="0" width="300%" height="100%" patternUnits="userSpaceOnUse">
                <rect x="0" y="0" width="150%" height="100%" fill="url(#gradient)">
                  <animate attributeType="XML" attributeName="x" from="0" to="150%" dur="10s" repeatCount="indefinite" />
                </rect>
                <rect x="-150%" y="0" width="150%" height="100%" fill="url(#gradient)">
                  <animate attributeType="XML" attributeName="x" from="-150%" to="0" dur="10s" repeatCount="indefinite" />
                </rect>
              </pattern>
            </defs>
          </svg>
        </div>
        <div class="col-span-2 row-start-1 rounded-xl p-4 text-white"></div>

        <div class="row-start-2 rounded-xl relative mr-5">
          <div class="chat-notice mt-10 ml-5 relative w-full">
            <div class="header text-left px-5 py-1 absolute h-full w-full -top-8 -left-5 rounded-xl bg-violet-600 text-white">
              Latest Follower
            </div>
            <div class="message relative bg-white rounded-xl rounded-b-xl overflow-hidden py-3 px-5">
              &nbsp;
            </div>
          </div>
        </div>

        <div class="row-start-2 rounded-xl relative mr-5">
          <div class="chat-notice mt-10 ml-5 relative w-full">
            <div class="header text-left px-5 py-1 absolute h-full w-full -top-8 -left-5 rounded-xl bg-indigo-500 text-white">
              Latest Subscriber
            </div>
            <div class="message relative bg-white rounded-xl rounded-b-xl overflow-hidden py-3 px-5">
              &nbsp;
            </div>
          </div>
        </div>

        <div class="row-start-2 rounded-xl relative mr-5">
          <div class="chat-notice mt-10 ml-5 relative w-full">
            <div class="header text-left px-5 py-1 absolute h-full w-full -top-8 -left-5 rounded-xl bg-purple-500 text-white">
              Latest Donation
            </div>
            <div class="message relative bg-white rounded-xl rounded-b-xl overflow-hidden py-3 px-5">
              &nbsp;
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="m-4 ml-0 w-96">
      <div class="h-[51rem] mb-4 bg-[#ffffff20] rounded-xl">
        <Chatbox class="max-h-full !p-0" channel="epickittyxp" />
      </div>
      <div class="avatar-box row-span-1 aspect-[16/9] bg-purple-800 text-white rounded-xl overflow-hidden relative text-center p-4">
        <video class="w-[28rem] max-w-[initial] aspect-[16/9] -m-8 absolute z-1" src="https://lok.surf/ead9795d-8d60-3662-bd02-7af9c1cc1a48" autoplay autofocus loop></video>
<!--        <span class="z-10 relative block mt-16">EpicKitty has escaped containment!<br>If found, return here!</span>-->
      </div>
    </div>
  </div>
</template>
<script setup>
import Chatbox from "../components/Chatbox.vue";
</script>
<style scoped>
.avatar-box {
  box-shadow: 1px -9px 29px -7px rgba(0,0,0,0.75) inset;
}
</style>