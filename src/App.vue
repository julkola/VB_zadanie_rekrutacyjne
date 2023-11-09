<script setup>
import { onMounted, watch, ref } from 'vue';
import Posts from './components/Posts.vue';
import Popup from './components/Popup.vue';
import Drop from './components/Drop.vue';

async function fetchUsers() {
  const response = await fetch('https://jsonplaceholder.typicode.com/users');
  const responseJson = await response.json();
  const users = new Map(responseJson.map((user) => [ user.id, user.name ]))
  return users;
}
const users = ref();

onMounted(async () => {
  users.value = await fetchUsers();
})
</script>

<template>
  <main>
    <header>
      <h1>
        Posts
      </h1>
      <Drop :users="users"/>
    </header>
    <Suspense>
      <Posts  :users="users"/>
      <template #fallback>
        <div class="loading-indicator">
          Loading...
        </div>
      </template>
    </Suspense>
    <Popup />
  </main>
</template>