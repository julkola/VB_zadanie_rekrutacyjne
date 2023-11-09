<script setup>
import { watch, ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();

const { users } = defineProps(["users"]);

async function fetchPosts() {
  const url  = route.params.id ?   `users/${route.params.id}/posts` : 'posts';
  const response = await fetch(`https://jsonplaceholder.typicode.com/${url}`);
  const posts = await response.json();
  return posts;
}

const posts = ref(await fetchPosts());

const isReloading = ref(false);

watch(
  () => route.params.id,
  async () => {
    isReloading.value = true;
    posts.value = await fetchPosts();
    isReloading.value = false;
  }
)
</script>

<template>
  <main>
    <div
      v-if="isReloading"
      class="loading-indicator"
    >
      Loading...
    </div>
    <div v-for="post in posts">
      <h2>
        {{ post.title }}
      </h2>
      <span>
        by&nbsp;
      </span>
      <b>
        {{ users ? users.get(post.userId) : '...' }}
      </b>
      <p>
        {{ post.body }}
      </p>
    </div>
  </main>
</template>