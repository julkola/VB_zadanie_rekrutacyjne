<script setup>
import { ref } from 'vue';

const isOpen = ref(false);
</script>
<template>
    <button
        @click="isOpen = true"
        class="icon"
        aria-haspopup="true"
    >
        i
    </button>
    <Teleport to="body">
        <Transition name="popup">
            <div
                v-if="isOpen"
                class="bg"
                @click.self="isOpen = false"
            >
                <div class="popup">
                    <picture>
                        <source
                            srcset="/src/assets/mountain-lg.jpg"
                            media="(min-width: 800px)"
                        >
                        <img
                            class="img"
                            src="/src/assets/mountain-sm.jpg"
                            alt="mountain picture"
                        >
                    </picture>
                    <span class="info-popup">
                        Info popup
                    </span>
                    <button @click="isOpen = false" class="close-btn">
                        Close
                    </button>
                </div>
            </div>
        </Transition>
    </Teleport>
</template>