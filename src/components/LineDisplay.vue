<template>
  <div :class="[`line-${line.state}`, { 'line-selected' : line.selected}]" :data-line-id="lineId">
    <strong class="mr-2 shrink-0" v-if="line.actor && line.state != 'hide'">{{ line.actor }}:</strong>
    <span v-if="line.state != 'hide' && !hideText">
      <span v-if="line.setting" class="italic mr-1">({{ line.setting }})</span><span>{{ line.text }}</span>
    </span>
    <button v-if="line.state!='hide' && line.state!='highlight' && hideText" @click="toggleHideText" class="show-text-button">Show</button>
    <button v-if="line.state=='highlight' && hideText" @click="toggleHideText" class="show-text-button">Show</button>
    <span v-if="line.state=='hide'">*</span>
  </div>
</template>

<script>
export default {
  name: 'LineDisplay',
  props: {
    line: {
      type: Object,
      required: true
    },
    lineId: {
      type: String,
      required: true
    },
    hideToCheck: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      hideText: this.hideToCheck && (this.line.state == 'show' || this.line.state == 'highlight')
    }
  },
  watch: {
    hideToCheck(newVal) {
      this.hideText = newVal && (this.line.state == 'show' || this.line.state == 'highlight');
    }
  },
  methods: {
    toggleHideText() {
      this.hideText = !this.hideText;
    }
  }
}
</script>

<style scoped>
/* Add your styles here */
</style>
