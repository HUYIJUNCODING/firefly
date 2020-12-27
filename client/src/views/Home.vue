<template>
    <div class="home">
        {{ name }}
    </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
    setup() {
        const name = ref('hello-firefly');

        return {
            name
        };
    }
});
</script>
