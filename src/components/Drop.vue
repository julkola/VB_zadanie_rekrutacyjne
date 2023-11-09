<script setup>
import { ref } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const { users } = defineProps(["users"]);

const isOpen = ref(false)
const currentUser = () => route.params.id ? +route.params.id : 'all';

</script>
<template>
    <div class="pseudoselect">
        <span class="dropdown-title">
            Authors:
        </span>
        <button
            class="select-head"
            @click="isOpen = !isOpen"
            :class="isOpen ? 'selected' : ''"
        >
            {{ users ? users.get(currentUser()) ?? 'All' : 'Loading...' }}
        </button>
        <div class="select-options" :class="isOpen ? '' : 'hide'">
            <RouterLink
                to="/"
                class="option"
                @click="isOpen = false"
                :class="currentUser() === 'all' ? 'selected' : ''"
            >
                All
            </RouterLink>
            <RouterLink
                @click="isOpen = false"
                class="option"
                v-for="[id, name] of users"
                :to="`/${id}`"
                :class="currentUser() === id ? 'selected' : ''"
            >
                {{ name }}
            </RouterLink>
        </div>
    </div>
</template>