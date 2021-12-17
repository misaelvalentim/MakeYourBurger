<template>
    <header class="header">
        <nav class="header__nav">
            <router-link to="/"><img src="https://raw.githubusercontent.com/matheusbattisti/curso_vue_yt/main/18_projeto/public/img/logo.png" class="header__logo"></router-link>
            <div class="header__menu" role="menu">
                <router-link to="/" class="menu__list">Home</router-link>
                <router-link to="/Pedidos" class="menu__list">Orders</router-link>
            </div>
            <span class="header__hamburger" role="menu" @click="hamburgerActive"></span>
        </nav>
    </header>
</template>
<script>
export default {
    name: 'navbar',
    methods: {
        hamburgerActive() {
            const menu = document.querySelector('.header__menu');
            const hamburgerActive = document.querySelector('.header__hamburger');
            menu.classList.toggle('active');
            hamburgerActive.classList.toggle('active');
        }
    }
}
</script>
<style scoped>
.header {
    width: 100%;
    background: #222f;
    
    border-bottom: 4px;
    border-color: #000000bb;
    border-style: solid;
}
.header__nav {
    width: 90%;
    height: 100%;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5em 0;
}
.header__logo {
    width: 30%;
    min-width: 40px;
}
.header__menu{
    position: absolute;
    left: 0;
    width: 0%;
    height: 0%;
    overflow: hidden;
    transform: translate(-350px);
    transition:all .5s ease-in-out;    
}
.menu__list {
    text-decoration: none;
    color:#FDBD18;
    font-size: 1.5em;
    margin: 0 .5em;
    text-shadow: 5px 5px 5px #000000e7;
}
.header__hamburger {
    width: 40px;
    border-top: 3px;
    border-style: solid;
    border-color: white;
    position: relative;
    cursor: pointer;
    padding: 0 0 1em;
    z-index: 1;
}
.header__hamburger::before {
    position: absolute;
    content: '';
    left: 0;
    top: 5px;
    width: inherit;
    border: inherit;
    transition: all .5s ease-in-out;
}
.header__hamburger::after {
    position: absolute;
    content: '';
    width: inherit;
    left: 0;
    top: 12px;
    border: inherit;
    transition: all .5s ease-in-out;
}

.header__menu.active {
    position: fixed;
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 100%;
    top: 0;
    background: #222;
    transform: translate(0);
    z-index: 0;
}
.header__menu.active .menu__list {
   width: 75%;
   text-align: center;
   padding: .2em;
   margin: 0 0 1em 1em;
   border: 1px solid white;
   border-radius: 10px;
   transition: all .5s ease-in-out;
}
.header__menu.active .menu__list:first-of-type {
   margin-top: 1em;
}
.header__menu.active .menu__list:hover {
    background: white;
    color: #333;
    padding: .2em 0;
    text-shadow: none;
}
.header__hamburger.active {
    border-color: transparent;
    position: fixed;
    right: 25px;
}
.header__hamburger.active::before {
    width: 30px;
    border-color: white;
    transform:skewY(45deg);
    top: 0;
    transition: all .5s ease-in-out;
}
.header__hamburger.active::after {
    border-color: white;
    width: 30px;
    top: 0;
    transform: skewY(-45deg);
    transition: all .5s ease-in-out;

}

@media only screen and (min-width: 768px) {
    .header__menu.active {
        display: none;
    }
    .header__hamburger {
        display: none;
    }
    .header__menu{
        position: initial;
        width: fit-content;
        overflow: initial;
        transform: none;
        transition: none;
    }
    .header__menu .menu__list:hover {
        color: #fdbc18a8;
    }
}
@media only screen and (min-width: 1200px) {
    
}
</style>