<script>
import sanitize from 'sanitize-html';
import Prompt from '../prompt.vue';

export default {
  components: {
    Prompt,
  },
  props: {
    count: {
      type: Number,
      required: true,
    },
    rawCode: {
      type: String,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    },
  },
  computed: {
    sanitizedOutput() {
      return sanitize(this.rawCode, {
        allowedTags: sanitize.defaults.allowedTags.concat(['img', 'svg']),
        allowedAttributes: {
          img: ['src'],
        },
      });
    },
    showOutput() {
      return this.index === 0;
    },
  },
};
</script>

<template>
  <div class="output">
    <prompt type="Out" :count="count" :show-output="showOutput" />
    <div v-html="sanitizedOutput"></div>
  </div>
</template>
