<template>
    <div class="burger-table">
        <Message :message="message" v-show="message"/>
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações</div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
                <div class="order-number">{{burger.id}}</div>
                <div>{{burger.name}}</div>
                <div>{{burger.bread}}</div>
                <div>{{burger.meat}}</div>
                <div>
                    <ul>
                        <li v-for="(optional, index) in burger.opcionais" :key="index">{{optional}}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updateBurger($event, burger.id)">
                        <option :value="s.type" v-for="s in status" :key="s.id" :selected="burger.status == s.type">
                            {{ s.type }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import Message from '../components/message.vue'
export default {
    name: 'dashboard',
    data(){
        return {
            burgers: null,
            burder_id: null,
            status: [],
            message: null
        }
    },
    components: {
        Message
    },
    methods: {
        async getPedidos(){
            const req = await fetch('http://localhost:3000/burgers');

            const data = await req.json();

            this.burgers = data;

            // resgatar status

            this.getStatus();
        },
        async getStatus(){
            const req = await fetch('http://localhost:3000/status');
            const data = await req.json();
            this.status = data;

        },
        async deleteBurger(id) {
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });
            const res = await req.json();

            // Msg ao deletarem

            // Colocar uma mensagem de sistema para usuario saber que foi enviado
            this.message = `Pedido removido com sucesso.`;

            // Limpar mensagem

            setTimeout( () => {
                this.message = '';
            }, 4000)

            this.getPedidos();

        },
        async updateBurger(event, id){
            const option = event.target.value;

            const dataJson = JSON.stringify({status: option});
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type" : "application/json"},
                body: dataJson
            });

            const res = await req.json();

            // Colocar uma mensagem de sistema para usuario saber que foi enviado
            this.message = `O pedido nº ${res.id} foi atualizado para ${res.status}.`;

            // Limpar mensagem
            setTimeout( () => {
                this.message = '';
            }, 4000)
        }
    },
    mounted(){
        this.getPedidos();
    }
}
</script>
<style scoped>
.burger-table {
    max-width: 1200px;
    margin: 0 auto;
}
#burger-table-heading, #burger-table-rows, .burger-table-row {
    display: flex;
    flex-wrap: wrap;
}
#burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}
#burger-table-heading div, .burger-table-row div {
    width: 19%;
}
.burger-table-row{
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
}

#burger-table-heading .order-id, .burger-table-row .order-number {
    width: 5%;
}

select {
    padding: 12px 0px;
    margin-right: 10px;
}
.delete-btn {
    background: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    padding: 12px 6px;
    transition: .5s;
}
.delete-btn:hover{
    background: transparent;
    color: #222;
}
</style>