<template>
  <Input
    v-bind="$props"
    :type="computedType"
    :icon-right="icon"
    class="mag-input-password"
    @update:modelValue="handleInput"
  >
    <template #icon-right>
      <Icon
        :icon="icon"
        class="mag-input-password-toggle"
        @click="toggle"
      />
    </template>
  </Input>
</template>

<script lang="ts">
import { computed, defineComponent, ref } from 'vue'
import Input from '../input/Input.vue'
import Icon from '../icon/Feather.vue'

export default defineComponent({
  name: 'MInputPassword',
  components: {
    Icon,
    Input,
  },
  props: {
    modelValue: {
      type: String,
      default: null,
    },
  },
  emits: ['change', 'update:modelValue'],
  setup: (_, { emit }) => {

    const hidePassword = ref(true)
    const icon = ref('eye-off')

    const computedType = computed(() => {
      return hidePassword.value ? 'password' : 'text'
    })
    
    const toggle = () => {
      hidePassword.value = !hidePassword.value
      icon.value = hidePassword.value ? 'eye-off' : 'eye'
    }

    const handleInput = (value: string) => {
      emit('change', value)
      emit('update:modelValue', value)
    }

    return { computedType, handleInput, toggle, hidePassword, icon }
  },
})
</script>

<style lang="scss" scoped>

@import '@magenta-ui/styles/scss/variables.scss';

.mag-input-password {
  
  .mag-input-password-toggle {
    color: $font-color-contrast;
    cursor: pointer;
  }
}
</style>
