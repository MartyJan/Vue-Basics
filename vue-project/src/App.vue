<script lang="ts">
// Import components
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: { Modal }, // Register components
  data() {
    return {
      key: 'value',
      books: ['book1', 'book2', 'book3'],
      url: 'https://www.google.com',
      isActive: true,

      email: '',
      role: 'admin', // Default value
    }
  },
  computed: {
    computedKey() {
      return this.key.toUpperCase()
    },
  },
  methods: {
    foo() {
      console.log('foo')
    },
    handleEvent(e: Event, arg?: unknown) {
      console.log(e)
      console.log(arg)
    },
    handleInput() {
      console.log((this.$refs.refName as HTMLInputElement).value)
    },
    submitForm() {
      console.log(this.email)
      console.log(this.role)
    },
  },
  // Lifecycle Hooks
  // https://vuejs.org/guide/essentials/lifecycle
  mounted() {
    console.log('mounted')
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
  <div @mouseover="handleEvent" class="eventBlock">mouseover</div>
  <!-- Event object should be passed explicitly when there are arguments -->
  <div @mousemove="handleEvent($event, 5)" class="eventBlock">mousemove</div>

  <!-- Event Modifiers -->
  <h1>Event Modifiers</h1>
  <div @click.right="handleEvent($event)" class="eventBlock">Right click</div>

  <!-- Conditional rendering -->
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
