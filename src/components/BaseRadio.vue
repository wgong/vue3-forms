<template>
  <input
      type="radio"
      v-bind="{ ...$attrs, onChange: updateValue }"
      :checked="modelValue === value"
      :id="uuid"
    />
  <label
    v-if="label"
    :for="uuid"
  >
    {{ label }}
  </label>
  <BaseErrorMessage
    v-if="error"
    :id="`${uuid}-error`"
  >
    {{ error }}
  </BaseErrorMessage>
</template>

<script>
import SetupFormComponent from '../features/SetupFormComponent.js'
import UniqueID from '../features/UniqueID.js'
import BaseErrorMessage from './BaseErrorMessage.vue'

export default {
  components : {
    BaseErrorMessage
  },

  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number]
    },
    value: {
      type: [String, Number]
    },
    error: {
      type: String,
      default: ''
    }
  },
  setup (props, context) {
    const uuid = UniqueID().getID()
    const { updateValue } = SetupFormComponent(props, context)

    return {
      updateValue,
      uuid
    }
  }
}
</script>
