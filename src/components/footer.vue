<template>
    <footer class="footer">
        <p class="footer__rights">Make Your Burger &copy; 2021</p>
    </footer>
</template>
<script>
export default {
    name: 'footer'
}
</script>
<style scoped>
.footer {
    width: 100%;
    min-height: 200px;
    background: #333;
    color: #FDBD18;
    display: flex;
    align-items: center;
    justify-content: center;
    border-top: 4px;
    border-style: solid;
    border-color: #000000;
}
.footer__rights {
    font-size: 1.5em;
}
@media only screen and (min-width: 768px) {
    .footer__rights {
        font-size: 2em;
    }
}
</style>