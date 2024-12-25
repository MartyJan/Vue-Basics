<script lang="ts">
import { ref, reactive, computed, onMounted, watch, watchEffect } from 'vue'
// Import components
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: { Modal },  // Register components
  setup() {
    // Data
    const key = ref('value')
    const books = reactive(['book1', 'book2', 'book3'])
    const url = ref('https://www.google.com')
    const isActive = ref(true)

    const email = ref('')
    const role = ref('admin') // Default value

    const refName = ref<HTMLInputElement | null>(null)

    // Computed
    const computedKey = computed(() => key.value.toUpperCase())

    // Methods
    const foo = () => {
      console.log('foo')
    }

    const handleEvent = (e: Event, arg?: unknown) => {
      console.log(e)
      console.log(arg)
    }

    const handleInput = () => {
      console.log(refName.value?.value)
    }

    const submitForm = () => {
      console.log(email.value)
      console.log(role.value)
    }

    // Lifecycle Hooks
    onMounted(() => {
      console.log('mounted')
    })

    // ref vs. reactive
    const objectReactive = reactive({
      name: 'John',
      age: 30,
    })
    const objectRef = ref({
      name: 'John',
      age: 30,
    })

    objectReactive.name = 'Doe' // Works
    objectRef.value.name = 'Doe' // Works

    const primitiveReactive = reactive(10)
    const primitiveRef = ref(10)

    // primitiveReactive = 20 // Doesn't work
    // primitiveReactive = reactive(20) // Doesn't work
    primitiveRef.value = 20 // Works

    // watch vs. watchEffect
    const stopWatch = watch(email, () => {
      console.log('email changed to ', email.value)
    })

    const stopWatchEffect = watchEffect(() => {
      console.log('email changed to', email.value)
      console.log('role changed to', role.value)
    })

    const handleWatch = () => {
      stopWatch()
      stopWatchEffect()
    }

    return {
      key,
      books,
      url,
      isActive,
      refName,
      email,
      role,
      computedKey,
      foo,
      handleEvent,
      handleInput,
      submitForm,
      objectReactive,
      objectRef,
      primitiveReactive,
      primitiveRef,
      handleWatch,
    }
  },
}
</script>

<template>
  <!-- Data -->
  <h1>Data</h1>
  <p>{{ key }}</p>

  <!-- Computed Properties -->
  <h1>Computed Properties</h1>
  <p>{{ computedKey }}</p>

  <!-- Events -->
  <h1>Events</h1>
  <div v-on:click="foo" class="eventBlock">click</div>
  <div @click="foo" class="eventBlock">click</div>
  <!-- Event object is passed automatically -->
  <div @mouseover="handleEvent($event)" class="eventBlock">mouseover</div>
  <!-- Event object should be passed explicitly when there are arguments -->
  <div @mousemove="handleEvent($event, 5)" class="eventBlock">mousemove</div>

  <!-- Event Modifiers -->
  <h1>Event Modifiers</h1>
  <div @click.right="handleEvent($event)" class="eventBlock">Right click</div>

  <!-- Conditional Rendering -->
  <h1>Conditional Rendering</h1>
  <p v-if="true">This is shown.</p>
  <p v-if="false">This is not shown.</p>

  <!-- List Rendering -->
  <h1>List Rendering</h1>
  <ul>
    <li v-for="(book, index) in books" :key="index">{{ book }}</li>
  </ul>

  <!-- Attribute Binding -->
  <h1>Attribute Binding</h1>
  <a v-bind:href="url" class="block">link</a>
  <a :href="url" class="block">link</a>

  <!-- Dynamic Classes -->
  <h1>Dynamic Classes</h1>
  <div :class="{ active: isActive }">Active</div>

  <!-- Template Refs -->
  <h1>Template Refs</h1>
  <input type="text" ref="refName" />
  <button @click="handleInput">Submit</button>

  <!-- VModel -->
  <h1>VModel</h1>
  <form @submit.prevent="submitForm">
    <p>Email:</p>
    <input type="email" v-model="email" />
    <p>Role:</p>
    <select v-model="role">
      <option value="admin">Admin</option>
      <option value="user">User</option>
    </select>
    <p></p>
    <button type="submit">Submit</button>
  </form>

  <!-- Components-->
  <!-- Props, Emit Custom Events, Slots, and Named Slots -->
  <h1>Components</h1>
  <Modal title="Hello World!" @customEvent="foo">
    <p>Content</p>
    <template v-slot:links>
      <a href="#" class="block">link 1</a>
      <a href="#" class="block">link 2</a>
    </template>
  </Modal>

  <!-- ref vs. reactive -->
  <h1>ref vs. reactive</h1>
  <p>objectReactive.name: {{ objectReactive.name }}</p>
  <p>objectRef.name: {{ objectRef.name }}</p>
  <p>primitiveReactive: {{ primitiveReactive }}</p>
  <p>primitiveRef: {{ primitiveRef }}</p>

  <!-- Stop Watch -->
  <h1>Stop Watch</h1>
  <button @click="handleWatch">Stop</button>
</template>

<!-- Scoped Style -->
<!-- Vue add additional attribute to html tags with scoped styles -->
<!-- This makes the styles only apply to the current component -->
<style scoped>
.active {
  background-color: red;
}

.block {
  display: block;
}

.eventBlock {
  background-color: lightblue;
  width: 200px;
  height: 100px;
  margin: 20px;
  text-align: center;
  cursor: pointer;
}
</style>
