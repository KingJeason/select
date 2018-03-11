<template>
<transition name="bl-zoom-in-center">
  <span class="bl-tag" :style="{backgroundColor: color}">
      <slot></slot>
      <img
        class="bl-icon-close"
        src="../assets/icons/close.png"
        v-if="closable"
        @click.stop="handleClose">
    </span>
</transition>
</template>

<script>
export default {
  name: 'BlTag',
  props: {
    text: String,
    closable: Boolean,
    color: String,
  },
  methods: {
    handleClose(event) {
      this.$emit('close', event);
    }
  },
  computed: {}
}
</script>

<style>
.bl-tag {
  cursor: text	;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #2873df;
  padding: 0 10px;
  height: 20px;
  line-height: 20px;
  font-size: 12px;
  color: white;
  border-radius: 4px;
  box-sizing: border-box;
  border: 1px solid rgba(64, 158, 255, .2);
  margin: 5px 5px 5px 0px;
}

.bl-tag .bl-icon-close {
  border-radius: 50%;
  text-align: center;
  position: relative;
  cursor: pointer;
  font-size: 12px;
  height: 10px;
  width: 10px;
  line-height: 10px;
  vertical-align: middle;
  top: -1px;
  right: -5px;
  color: #409EFF
}
</style>
