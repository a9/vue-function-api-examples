<template>
  <div class="home">
    {{ count }}

    <span>{{ x }} {{ y }}</span>
    <div>{{ width }} {{ height }}</div>
    <ui-button @click="add">
      ss
    </ui-button>
  </div>
</template>

<script lang="ts">
import { onMounted, onUnmounted, value } from 'vue-function-api'
import UiButton from '@/views/button.vue'

function useCount() {
  let count = value(0)

  const add = () => {
    count.value++
  }
  return {
    count,
    add
  }
}

function useMouse() {
  const x = value(0)
  const y = value(0)

  const update = (e: MouseEvent) => {
    x.value = e.pageX
    y.value = e.pageY
  }
  onMounted(() => {
    window.addEventListener('mousemove', update)
  })
  onUnmounted(() => {
    window.removeEventListener('mousemove', update)
  })
  return { x, y }
}

function useWindowResize() {
  const width = value(window.innerWidth)
  const height = value(window.innerHeight)

  const update = (e: UIEvent) => {
    width.value = window.innerWidth
    height.value = window.innerHeight
  }

  onMounted(() => {
    window.addEventListener('resize', update)
  })
  onUnmounted(() => {
    window.removeEventListener('resize', update)
  })
  return { width, height }
}

export default {
  components: { UiButton },
  setup() {
    const { count, add } = useCount()
    const { x, y } = useMouse()
    const { width, height } = useWindowResize()

    return {
      count,
      add,
      x,
      y,
      width,
      height
    }
  }
}
</script>
