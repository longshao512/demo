<template>
  <div>
    <!-- 颜色组件 -->
    <Color></Color>
    <!-- 模式组件 -->
    <Theme></Theme>
  </div>
</template>

<script>
import Color from '@/components/Form/color.vue'
import Theme from '@/components/Form/theme.vue'

export default {
  name: 'Home',
  components: {
    Theme:Theme,
    Color:Color
  }
}
</script>