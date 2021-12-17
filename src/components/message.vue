<template>
    <p class="form__message">{{message}}</p>
</template>
<script>
export default {
    name: 'message',
    props: {
        message: String
    }
}
</script>
<style scoped>
    .form__message {
        background: #333;
        color: #FDBD18;
        font-size: 1.2em;
        border-radius: .7em;
        text-align: left;
        padding:  .8em .7em;
        margin-bottom: 1em;
        text-align: center;
    }
</style>