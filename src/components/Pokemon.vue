<template>
    <div>
        <h1>{{ num }}-{{ name }}</h1>
        <p>{{ url }}</p>
    </div>
</template>

<script>
export default {
    name: 'Pokemon',
    props: {
        name: String,
        url: String,
        num: Number
    }
}
</script>

<style scoped>
    h1 {
        text-transform: capitalize;
    }
</style>