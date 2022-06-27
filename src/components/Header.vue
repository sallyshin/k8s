<template>
    <header>
        <h1>{{ title }}</h1>
        <Button :custom_text="isFormShown ? 'CLOSE' : 'ADD'" :custom_color="isFormShown ? 'red' : 'green'" @btn-click="$emit('change-mode')"></Button>
    </header>
</template>

<script>
import Button from './Button'

export default {
    name: 'Header',
    props: {
        title: String,
        isFormShown: Boolean
    },
    components: {
        Button
    },
    emits: ['change-mode']
}
</script>

<style>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>