<template>
  <svg class="inline ml-2" :class="classes" width="512" height="512" viewBox="0 0 512 512" style="color:currentColor" xmlns="http://www.w3.org/2000/svg"><rect width="512" height="512" x="0" y="0" rx="30" fill="transparent" stroke="transparent" stroke-width="0" stroke-opacity="100%" paint-order="stroke"></rect><svg width="512px" height="512px" viewBox="0 0 24 24" fill="currentColor" x="0" y="0" role="img" style="display:inline-block;vertical-align:middle" xmlns="http://www.w3.org/2000/svg"><g fill="currentColor"><path fill="currentColor" fill-rule="evenodd" d="M6.535 3.25a1.75 1.75 0 0 0-1.456.78L1.49 9.412c-.219.33-.245.752-.068 1.106A32.952 32.952 0 0 0 9.45 20.8l1.75 1.501a1.23 1.23 0 0 0 1.601 0l1.75-1.5a32.951 32.951 0 0 0 8.029-10.283c.177-.354.15-.776-.069-1.106L18.92 4.03a1.75 1.75 0 0 0-1.455-.779H6.535Zm-.208 1.611a.25.25 0 0 1 .208-.111h2.34L6.96 9.346a1.75 1.75 0 0 0-.1.326a69.284 69.284 0 0 1-2.11-.19l-1.405-.147L6.327 4.86ZM3.28 10.836a31.45 31.45 0 0 0 6.994 8.695l-3.125-8.334a70.78 70.78 0 0 1-2.554-.222l-1.315-.139Zm5.506.454L12 19.864l3.215-8.574a70.793 70.793 0 0 1-6.43 0Zm8.067-.093l-3.125 8.334a31.45 31.45 0 0 0 6.994-8.695l-1.315.139c-.85.089-1.701.163-2.554.222Zm3.803-1.862l-1.406.148a69.27 69.27 0 0 1-2.11.19a1.747 1.747 0 0 0-.099-.327L15.125 4.75h2.34a.25.25 0 0 1 .208.111l2.982 4.474Zm-5.063.435c-2.393.124-4.79.124-7.184 0L10.5 4.75h3l2.092 5.02Z" clip-rule="evenodd"/></g></svg></svg>
</template>
<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  classes: {
    type: Object,
    required: false,
    default: () => ({
      'w-5': true,
      'h-5': true,
      'text-teal-300': true,
    })
  }
});
</script>