<template>
    <input type="number" :name="inputNumberName" :id="inputNumberId">
</template>
<script>
export default {
    name: 'inputNumber',
    props: {
        inputNumberName: String,
        inputNumberId: String
    }
}
</script>