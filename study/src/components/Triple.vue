<template>
    <button @click="increment">
        Count is : {{state.count}} , triple is : {{state.triple}}
    </button>
</template>

<script>
import { reactive, computed } from '@vue/composition-api'

export default {
    setup() {
        const state = reactive({
            count: 0,
            triple: computed(() => state.count *3)
        })

        function increment() {
            state.count ++;
        }

        return {
            state,
            increment
        }
    },
}
</script>
