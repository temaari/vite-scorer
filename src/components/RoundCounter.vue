<template>
    <div>
        <p>Current Round: {{ current }}</p>
    </div>
</template>

<script>
    export default {
        name: 'RoundCounter',
        props: {
            current: {
                type: Number,
                default: 0
            }
        }
    }
</script>

<style scoped>
</style>