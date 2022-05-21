<template>
  <div>
    <Color></Color>
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