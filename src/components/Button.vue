<template>
    <button class="btn" :style="{ background: custom_color }" @click="onClick">{{ custom_text }}</button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        custom_text: String,
        custom_color: String
    },
    emits: ['btn-click'],
    methods: {
        onClick() {
            this.$emit('btn-click')
        }
    }
}
</script>