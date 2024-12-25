# Vue Basics

## Data

```vue
<template>
  <!-- Data -->
  <p>{{ key }}</p>
</template>
```

### Composition API: `<script setup>`

```vue
<script setup lang="ts">
import { ref, reactive } from "vue";

const key = ref("value");
const books = reactive(["book1", "book2", "book3"]);
const url = ref("https://www.google.com");
const isActive = ref(true);

const email = ref("");
const role = ref("admin"); // Default value
</script>
```

### Copmosition API: `setup()`

```vue
<script lang="ts">
import { ref, reactive } from "vue";

export default {
  setup() {
    const key = ref("value");
    const books = reactive(["book1", "book2", "book3"]);
    const url = ref("https://www.google.com");
    const isActive = ref(true);

    const email = ref("");
    const role = ref("admin"); // Default value

    return {
      key,
      books,
      url,
      isActive,
      email,
      role,
    };
  },
};
</script>
```

### Options API

```vue
<script lang="ts">
export default {
  data() {
    return {
      key: "value",
      books: ["book1", "book2", "book3"],
      url: "https://www.google.com",
      isActive: true,

      email: "",
      role: "admin", // Default value
    };
  },
};
</script>
```

## Computed Properties

Data that depends on other data

```vue
<template>
  <!-- Computed Properties -->
  <p>{{ computedKey }}</p>
</template>
```

### Composition API: `<script setup>`

```vue
<script setup lang="ts">
import { computed } from "vue";
const computedKey = computed(() => key.value.toUpperCase());
</script>
```

### Copmosition API: `setup()`

```vue
<script setup lang="ts">
import { computed } from "vue";

export default {
  setup() {
    const computedKey = computed(() => key.value.toUpperCase());

    return {
      computedKey,
    };
  },
};
</script>
```

### Options API

```vue
<script lang="ts">
export default {
  computed: {
    computedKey() {
      return this.key.toUpperCase();
    },
  },
};
</script>
```

## Methods

### Composition API: `<script setup>`

```vue
<script setup lang="ts">
const foo = () => {
  console.log("foo");
};

const handleEvent = (e: Event, arg?: unknown) => {
  console.log(e);
  console.log(arg);
};

const submitForm = () => {
  console.log(email.value);
  console.log(role.value);
};
</script>
```

### Copmosition API: `setup()`

```vue
<script lang="ts">
export default {
  setup() {
    const foo = () => {
      console.log("foo");
    };

    const handleEvent = (e: Event, arg?: unknown) => {
      console.log(e);
      console.log(arg);
    };

    const submitForm = () => {
      console.log(email.value);
      console.log(role.value);
    };

    return {
      foo,
      handleEvent,
      submitForm,
    };
  },
};
</script>
```

### Options API

```vue
<script lang="ts">
export default {
  methods: {
    foo() {
      console.log("foo");
    },
    handleEvent(e: Event, arg?: unknown) {
      console.log(e);
      console.log(arg);
    },
    submitForm() {
      console.log(this.email);
      console.log(this.role);
    },
  },
};
</script>
```

## Lifecycle Hooks

### Composition API: `<script setup>`

```vue
<script setup lang="ts">
import { onMounted } from "vue";

onMounted(() => {
  console.log("mounted");
});
</script>
```

### Copmosition API: `setup()`

```vue
<script lang="ts">
import { onMounted } from "vue";

export default {
  setup() {
    onMounted(() => {
      console.log("mounted");
    });
  },
};
</script>
```

### Options API

```vue
<script lang="ts">
export default {
  mounted() {
    console.log("mounted");
  },
};
</script>
```

## Events and Event Modifiers

```vue
<template>
  <!-- Events -->
  <div v-on:click="foo" class="eventBlock">click</div>
  <div @click="foo" class="eventBlock">click</div>

  <!-- Event object is passed automatically -->
  <div @mouseover="handleEvent" class="eventBlock">mouseover</div>
  <!-- Event object should be passed explicitly when there are arguments -->
  <div @mousemove="handleEvent($event, 5)" class="eventBlock">mousemove</div>

  <!-- Event Modifiers -->
  <div @click.right="handleEvent" class="eventBlock">right click</div>
</template>
```

## Conditional Rendering

```vue
<template>
  <!-- Conditional Rendering -->
  <p v-if="true">This is shown.</p>
  <p v-if="false">This is not shown.</p>
</template>
```

## List Rendering

```vue
<template>
  <!-- List Rendering -->
  <ul>
    <li v-for="(book, index) in books" :key="index">{{ book }}</li>
  </ul>
</template>
```

## Attribute Binding

```vue
<template>
  <!-- Attribute Binding -->
  <a v-bind:href="url" class="block">link</a>
  <a :href="url" class="block">link</a>
</template>
```

## Dynamic Classes

```vue
<template>
  <!-- Dynamic Classes -->
  <div :class="{ active: isActive }">Active</div>
</template>
```

## Template Refs

```vue
<template>
  <!-- Template Refs -->
  <input type="text" ref="refName" />
  <button @click="handleInput">Submit</button>
</template>
```

### Composition API: `<script setup>`

```vue
<script setup lang="ts">
const refName = ref<HTMLInputElement | null>(null);
const handleInput = () => {
  console.log(refName.value?.value);
};
</script>
```

### Copmosition API: `setup()`

```vue
<script lang="ts">
import { onMounted } from "vue";

export default {
  setup() {
    const refName = ref<HTMLInputElement | null>(null);
    const handleInput = () => {
      console.log(refName.value?.value);
    };
    return {
      handleInput,
    };
  },
};
</script>
```

### Options API

```vue
<script lang="ts">
export default {
  methods: {
    handleInput() {
      console.log((this.$refs.refName as HTMLInputElement).value);
    },
  },
};
</script>
```

### VModel

```vue
<template>
  <!-- VModel -->
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
</template>
```

## Components (Props, Emit Custom Events, Slots, Named Slots)

### App.vue

```vue
<template>
  <Modal title="Hello World!" @customEvent="foo">
    <p>Content</p>
    <template v-slot:links>
      <a href="#" class="block">link 1</a>
      <a href="#" class="block">link 2</a>
    </template>
  </Modal>
</template>
```

#### Composition API: `<script setup>`

```vue
<script setup lang="ts">
// Import components
import Modal from "./components/Modal.vue";
</script>
```

#### Composition API: `setup()`

```vue
<script lang="ts">
// Import components
import Modal from "./components/Modal.vue";

export default {
  components: { Modal }, // Register components
};
</script>
```

#### Options API

```vue
<script lang="ts">
// Import components
import Modal from "./components/Modal.vue";

export default {
  components: { Modal }, // Register components
};
</script>
```

### components/Modal.vue

```vue
<template>
  <!-- Props -->
  <p>{{ title }}</p>

  <!-- Emit Custom Events -->
  <button @click="emitEvent">Emit</button>

  <!-- Slots -->
  <slot></slot>

  <!-- Named Slots -->
  <slot name="links"></slot>
</template>
```

#### Composition API: `<script setup>`

```vue
<script setup lang="ts">
const props = defineProps<{
  title: string;
}>();

const emit = defineEmits<{
  (e: "customEvent"): void;
}>();

// Methods
const emitEvent = () => {
  emit("customEvent");
};

console.log(props);
</script>
```

#### Copmosition API: `setup()`

```vue
<script lang="ts">
export default {
  name: "Modal",
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  emits: ["customEvent"],
  setup(props, { emit }) {
    // Methods
    const emitEvent = () => {
      emit("customEvent");
    };

    console.log(props);

    return {
      emitEvent,
    };
  },
};
</script>
```

#### Options API

```vue
<script lang="ts">
export default {
  name: "Modal",
  props: ["title"], // Props
  emits: ["customEvent"], // Declare custom events
  methods: {
    emitEvent() {
      this.$emit("customEvent");
    },
  },
};
</script>
```

## `ref` vs. `reactive`

`ref`

- Used to create reactive references for both primitive values (e.g., numbers, strings, booleans) and objects.
- In the `<script>` section, you access or update the value using the .value property.
- In the `<template>` section, Vue automatically unwraps refs, allowing direct access without .value.

`reactive`

- Employed to create reactive objects or arrays.
- In the `<script>` section, you can access and update properties directly without the .value property.
- In the `<template>` section, properties are accessed directly as well.

### Composition API

```vue
<script setup lang="ts">
import { ref, reactive } from "vue";

const objectReactive = reactive({
  name: "John",
  age: 30,
});
const objectRef = ref({
  name: "John",
  age: 30,
});

objectReactive.name = "Doe"; // Works
objectRef.value.name = "Doe"; // Works

const primitiveReactive = reactive(10); // [Vue warn] value cannot be made reactive: 10
const primitiveRef = ref(10);

// primitiveReactive = 20 // Doesn't work
// primitiveReactive = reactive(20) // Doesn't work
primitiveRef.value = 20; // Works
</script>

<template>
  <!-- Ref vs. Reactive -->
  <p>objectReactive.name: {{ objectReactive.name }}</p>
  <p>objectRef.name: {{ objectRef.name }}</p>
  <p>primitiveReactive: {{ primitiveReactive }}</p>
  <p>primitiveRef: {{ primitiveRef }}</p>
</template>
```

## `watch` vs. `watchEffect`

- `watch` is called only when the watched source (i.e., `email` in the following example) changes.
- `watchEffect` runs once immediately after the component is set up and re-runs whenever any of its reactive dependencies (i.e., `email`, `role` in the following example) change.

### Composition API

```vue
<script setup lang="ts">
import { watch, watchEffect } from "vue";

const stopWatch = watch(email, () => {
  console.log("email changed to", email.value);
});

const stopWatchEffect = watchEffect(() => {
  console.log("email changed to", email.value);
  console.log("role changed to", role.value);
});

const handleWatch = () => {
  stopWatch();
  stopWatchEffect();
};
</script>
```
