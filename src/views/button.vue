<template>
  <div class="button" @click="click"><slot /></div>
</template>

<script lang="ts">
export default {
  name: 'ui-button',
  setup(props, context) {
    const click = (e: MouseEvent) => {
      context.emit('click', e)
    }

    return {
      click
    }
  }
}
</script>

<style lang="less"></style>
