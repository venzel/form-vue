<template>
    <div id="app">
        <h1>Registrar Reclamação</h1>
        <div class="conteudo">
            <form class="painel" v-if="!form_send">
                <div class="cabecalho">Formulário</div>
                <Rotulo nome="E-mail">
                    <input type="text" v-model.trim.lazy="data_user.email" />
                </Rotulo>
                <Rotulo nome="Senha">
                    <input type="password" v-model="data_user.password" />
                </Rotulo>
                <Rotulo nome="Idade">
                    <input type="number" v-model.number="data_user.age" />
                </Rotulo>
                <Rotulo nome="Mensagem">
                    <textarea name="" cols="30" rows="5" v-model="data_user.message"></textarea>
                </Rotulo>
                <Rotulo nome="Características do Problema">
                    <span class="mr-4"><input type="checkbox" value="reproduzivel" v-model="data_user.reproducible" /> Reproduzível</span>
                    <span><input type="checkbox" value="intermitente" v-model="data_user.reproducible" /> Intermitente</span>
                </Rotulo>
                <Rotulo nome="Qual produto?">
                    <span class="mr-4"><input type="radio" value="web" v-model="data_user.product" />Web</span>
                    <span class="mr-4"><input type="radio" value="mobile" v-model="data_user.product" />Mobile</span>
                    <span><input type="radio" value="other" v-model="data_user.product" />Outro</span>
                </Rotulo>
                <Rotulo nome="Prioridade">
                    <select v-model="priority">
                        <option v-for="p in priorities" :key="p.id" :value="p.slug" :selected="p.id === 1">{{ p.description }}</option>
                    </select>
                </Rotulo>
                <Rotulo nome="Primeira Reclamação?">
                    <Escolha v-model="choice" />
                </Rotulo>
                <hr />
                <button @click.prevent="send">Enviar</button>
            </form>
            <div class="painel" v-else>
                <div class="cabecalho">Resultado</div>
                <Rotulo nome="E-mail">
                    <span>{{ data_user.email }}</span>
                </Rotulo>
                <Rotulo nome="Senha">
                    <span>{{ data_user.password }}</span>
                </Rotulo>
                <Rotulo nome="Idade">
                    <span>{{ data_user.age }}</span>
                </Rotulo>
                <Rotulo nome="Mensagem">
                    <span style="white-space: pre">{{ data_user.message }}</span>
                </Rotulo>
                <Rotulo nome="Marque as Opções">
                    <ul>
                        <li v-for="(r, i) in data_user.reproducible" :key="i">{{ r }}</li>
                    </ul>
                </Rotulo>
                <Rotulo nome="Qual produto?">
                    <span>{{ data_user.product }}</span>
                </Rotulo>
                <Rotulo nome="Prioridade">
                    <span>{{ priority }}</span>
                </Rotulo>
                <Rotulo nome="Primeira Reclamação?">
                    <span>{{ choice ? 'sim' : 'nao' }}</span>
                </Rotulo>
            </div>
        </div>
    </div>
</template>

<script>
import Rotulo from './components/Rotulo.vue';
import Escolha from './components/Escolha.vue';

export default {
    name: 'app',
    components: { Rotulo, Escolha },
    data() {
        return {
            priorities: [
                { id: 1, slug: 'alta', description: 'Alta' },
                { id: 2, slug: 'baixa', description: 'Baixa' },
                { id: 3, slug: 'media', description: 'Media' },
            ],
            priority: 'alta',
            choice: false,
            form_send: false,
            data_user: {
                email: '',
                password: '',
                age: '',
                message: '',
                reproducible: [],
                product: 'web',
            },
        };
    },
    methods: {
        send() {
            this.form_send = true;
        },
    },
};
</script>

<style>
body {
    background-color: #ececec;
}

#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;

    display: flex;
    flex-direction: column;
}

.conteudo {
    display: flex;
}

.painel {
    flex: 1;
    background: #fff;
    margin: 0px 10px;
    padding: 20px;
    border: 1px solid #aaa;
    border-radius: 5px;
}

.painel .cabecalho {
    width: 100%;
    background-color: #ddd;
    padding: 10px 0px;
    border-radius: 5px;
    font-size: 1.4rem;
}

#app form button {
    float: right;
    margin: 10px 0px;
    padding: 10px 20px;
    font-size: 1.4rem;
    border-radius: 5px;
    color: #fff;
    background-color: #2196f3;
}

#app h1 {
    font-weight: 200;
    margin: 20px;
    padding: 0;
}

.mr-4 {
    margin-right: 40px;
}
</style>
