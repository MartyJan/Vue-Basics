<script lang="ts">
export default {
  name: 'Modal',
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  emits: ['customEvent'],
  setup(props, { emit }) {
    // Methods
    const emitEvent = () => {
      emit('customEvent')
    }

    console.log(props)

    return {
      emitEvent,
    }
  },
}
</script>

<template>
  <!-- Props -->
  <h2>Props</h2>
  <p>{{ title }}</p>

  <!-- Emit Custom Events -->
  <h2>Emit Events</h2>
  <button @click="emitEvent">Emit</button>

  <!-- Slots -->
  <h2>Slots</h2>
  <slot></slot>

  <!-- Named Slots -->
  <h2>Named Slots</h2>
  <slot name="links"></slot>
</template>
