<template>
    <section class="form">
        <form method="get" class="form__content" @submit="createBurger">
            <h2 class="form__title">Monte o seu burger:</h2>
            <Message :message="message" v-show="message"/>
            <label class="form__label">Nome do cliente:</label>
            <input type="text" name="name" class="inputTextClass" id="name" placeholder="Digite seu nome" v-model="name">
            <label class="form__label"> Escolha o pão:</label>
            <select name="select" class="selectBread" v-model="bread" required>
                <Option type="" Value="Select your bread" selected/>
                <option v-for="bread in breads" :key="bread.id" :value="bread.type">{{ bread.type }}</option>
            </select>
            <label class="form__label">Escolha a carne do seu Burger:</label>
            <select name="select" class="selectMeat" v-model="meat" required>
                <Option type="" Value="Select your meat" selected/>
                <option v-for="meat in meats" :key="meat.id" :value="meat.type"> {{ meat.type }}</option>
            </select>
            <label class="form__label"> Selecione os opcionais:</label>
            <div class="optional__content" >
                <div v-for="opcional in opcionaisdata" :key="opcional.id"> 
                      <input type="checkbox" name="opcional" id="opcionais" v-model="opcionais" :value="opcional.type">
                      <span>{{ opcional.type }}</span>
                </div>
            </div>
            <submit submitValue="Criar meu Burger!" submitClass="form__submit"/>
        </form>
  </section>
</template>
<script>
    import inputText from '../components/inputs/inputText.vue'
    import Option from '../components/inputs/Option.vue'
    import submit from '../components/inputs/submit.vue'
    import Message from '../components/message.vue'
export default {
    name: 'burgerForm',
    components: {
        inputText,
        Option,
        submit,
        Message
    },
    data(){
      return{
        breads: null,
        meats: null,
        opcionaisdata: null,
        name: null,
        bread: null,
        meat: null,
        opcionais: [],
        message: null,
        status: "Solicitado"
      }
    },
    methods: {
      async getIngredients(){
        const req = await fetch('http://localhost:3000/ingredients');

        const data = await req.json();

        this.breads = data.breads;
        this.meats = data.meats;
        this.opcionaisdata = data.opcionais,
        this.status = "Solicitado"
      },
      async createBurger(e) {
        e.preventDefault();

        const data = {
          name: this.name,
          meat: this.meat,
          bread: this.bread,
          opcionais: Array.from(this.opcionais)
        }

        const dataJson = JSON.stringify(data);

        const req = await fetch('http://localhost:3000/burgers', {
          method: "POST",
          headers: {"Content-Type": "application/json"},
          body: dataJson
        });

        const res = await req.json();

        // Colocar uma mensagem de sistema para usuario saber que foi enviado
        this.message = `Seu pedido nº ${res.id} foi efetuado com sucesso.`;

        // Limpar mensagem

        setTimeout( () => {
          this.message = '';
        }, 4000)

        // Limpar os campos após o usuário enviar o burger pro servidor
        this.name = "",
        this.meat = "",
        this.bread = "",
        this.opcionais = ""
      }
    },
    mounted() {
      this.getIngredients()
    }
}
</script>
<style scoped>
.form {
    width: 100%;
    height: fit-content;
    padding: 2em 0;
}
.form__title {
    font-size: 2.5em;
    padding-bottom: .5em;
}
.form__label {
    width: fit-content;
    border-left: 3px;
    border-style: solid;
    border-color: #FDBD18;
    font-size: 1.5em;
    padding: .3em 0 0 .2em;
    margin-bottom: .5em;
    line-height: 1.2em;
}
.form__content {
    max-width: 300px;
    margin: 0 auto;
    padding-left: 1em;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    text-align: left;
}
.selectBread, .selectMeat {
    width: 100%;
    min-width: 100px;
    max-width: 250px;
    margin-bottom: 1em;
    font-size: 1em;
    padding: .2em 0;
}
.inputTextClass {
    min-width: 100px;
    width: 100%;
    max-width: 240px;
    font-size: 1em;
    padding: .2em 0;
    margin: 0 0 1em 0;
}
.optional__content {
    display: grid;
    grid-template-columns: auto;
    grid-template-rows: auto;
    row-gap: 1.5em;
    column-gap: .5em;
    padding: 1em 0;
    transition: all .5s ease-in-out;
    font-size: 1.2em;
}
#form__submit {
    background: #333;
    color: #FDBD18;
    padding: .8em 2.5em;
    align-self: flex-start;
    font-size: 1em;
    cursor: pointer;
    transition: all .3s ease-in-out;
}
#form__submit:hover{
  background: transparent;
  color: #333;
}
@media only screen and (min-width: 768px) {
  .form__title {
    font-size: 4em;
    width: 100%;
  }
  .form__subtitle {
    width: fit-content;
    font-size: 2em;
    padding: .3em 0 0 .2em;
    margin-bottom: .5em;
  }
  .form__content {
    max-width: 400px;
  }
  .selectBread, .selectMeat {
    font-size: 1.2em;
  }
  .inputTextClass {
    font-size: 1.2em;
  }
  .optional__content {
    grid-template-columns: 1fr auto;
    column-gap: 4em;
  }
    #form__submit {
      padding: 1em 5em;
    }
  }
  @media only screen and (min-width: 1200px) {
    .optional__content {
      grid-template-columns: auto auto auto;
      column-gap: 1em;
    }
  }
</style>