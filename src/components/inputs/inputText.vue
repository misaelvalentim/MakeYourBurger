<template>
    <input type="text" :name="inputTextName" :class="inputTextClass" :placeholder="inputTextPlaceholder">
</template>
<script>
export default {
    name: 'inputNumber',
    props: {
        inputTextName: String,
        inputTextClass: String,
        inputTextPlaceholder: String
    }
}
</script>