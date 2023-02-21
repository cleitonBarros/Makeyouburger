<template>
    <div id="burger-table">
        <div>
            <div id="burguer-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pâo:</div>
                <div>carne:</div>
                <div>Opcionais:</div>
                <div>Açôes</div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div id="burger-table-row" v-for="burger in burgers" :key="burger.id">
                <div class="order-number">{{ burger.id }}</div>
                <div>{{ burger.nome }}</div>
                <div>{{ burger.pao }}</div>
                <div>{{ burger.carne }}</div>
                <div>
                    <ul>
                        <li v-for="(opcionais, index) in burger.opcionais" :key="index">{{ opcionais }}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status">
                        <option v-for="s in status" :key="s.id" value="s.tipo" :selected="burger.status === s.tipo"
                        >{{ s.tipo }}</option>
                    </select>
                    <button class="delete-btn">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        name: "Dashboard",
        data(){
            return{
                burger_Id:null,
                burgers: null,
                status: []
            }
        },
        methods:{
            async getBurger(){
                const req =  await fetch(" http://localhost:3000/burgers")
                const data = await req.json()

                this.burgers= data
                this.getStatus();
            },
            async getStatus(){
                const req = await fetch(" http://localhost:3000/status")
                const data = await req.json()

                this.status = data
            }
        },
        mounted(){
            this.getBurger()
        }
    }
</script>
<style scoped>
    #burger-table{
        max-width: 1200px;
        margin: 0 auto;
    }
    #burguer-table-heading,
    #burger-table-rows,
    #burger-table-row{
        display: flex;
        flex-wrap: wrap;
    }
    #burguer-table-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333; 
    }
    #burger-table-row{
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }
    #burguer-table-heading div,
    #burger-table-row div{
        width: 19%;
    }

    #burguer-table-heading .order-id, 
    #burger-table-row .order-number{
        width: 5%;;
    }
    select{
        padding: 12px 6px;
        margin-right: 12px;
    }
    .delete-btn{
        color: #fcba03;
        background-color: #222;
        font-weight:bold;
        font-size: 16px;
        padding: 10px;
        margin: 0 auto;
        border: 2px solid #222;
        cursor: pointer;
        transition: .5s;
    }
    .delete-btn:hover{
        background-color: transparent; 
        color: #222;
    }

</style>