<template>
    <input type="submit" :value="submitValue" :id="submitClass">
</template>
<script>
export default {
    name: 'inputNumber',
    props: {
        submitValue: String,
        submitClass: String
    }
}
</script>