<template>
  <Button
    v-bind="$attrs"
    :class="computedClasses"
    :disabled="props.disabled || props.loading"
    :loading="props.loading"
    :icon="props.icon"
    :iconPos="props.iconPos"
    :text="props.text"
    :severity="props.severity"
  >
    <template v-if="$slots.default">
      <slot />
    </template>
    <template v-else-if="props.label">
      {{ props.label }}
    </template>
  </Button>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import Button from 'primevue/button'

export interface DSButtonProps {
  label?: string
  icon?: string
  iconPos?: 'left' | 'right' | 'top' | 'bottom'
  severity?: 'primary' | 'secondary' | 'success' | 'info' | 'warning' | 'danger' | 'contrast' | 'help'
  text?: boolean
  size?: 'small' | 'medium' | 'large'
  disabled?: boolean
  loading?: boolean
}

const props = withDefaults(defineProps<DSButtonProps>(), {
  severity: 'primary',
  size: 'medium',
  disabled: false,
  loading: false,
  text: false
})

const computedClasses = computed(() => {
  const classes = ['ds-button']
  
  if (props.size) {
    classes.push(`ds-button--${props.size}`)
  }
  
  return classes
})
</script>

<style scoped>
.ds-button {
  @apply transition-all duration-500 ease-in-out;
}

.ds-button--small {
  @apply text-sm px-3 py-1;
}

.ds-button--medium {
  @apply text-base px-4 py-2;
}

.ds-button--large {
  @apply text-lg px-6 py-3;
}
</style>