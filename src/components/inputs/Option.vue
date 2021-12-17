<template>
    <option :value="type">{{Value}}</option>
</template>
<script>
export default {
    name: 'Option',
    props: {
        Option: String,
        Value: String
    }
}
</script>