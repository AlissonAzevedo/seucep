<template>
    <div class="container">
        <h1 class="title">SEU CEP</h1>
        <div class="containerInput">
            <input type="text" v-model="cepSearch" placeholder="Digite seu Cep..." />
            <button @click="searchCep" class="searchButton">
                <Search :size="28" class="searchIcon"/>
            </button>
        </div>
        <main class="main" v-if="isValid == true">
            <h2>Seu Cep: 
                <strong>
                    {{this.cep}}
                </strong>
            </h2>
            <span>Rua: 
                <strong>
                    {{this.logradouro}}
                </strong> 
            </span>
            <span>Complemento: 
                <strong>
                    {{this.complemento}}
                </strong> 
            </span>
            <span>Bairro: 
                <strong>
                    {{this.bairro}}
                </strong>
            </span>
            <span>Cidade: 
                <strong>
                    {{this.cidade}} 
                </strong>
                UF:
                <strong>
                    {{this.uf}}
                </strong>
            </span>
            <span>DDD: 
                <strong>
                    {{this.ddd}}
                </strong>
            </span>
        </main>
    </div>
</template>

<script>
import Search from "vue-material-design-icons/Magnify";
import api from "../services/api";
export default {
    name: "SearchCep",
    components: {
        Search,
    },
    data() {
        return {
            cepSearch: "",
            cep: "",
            logradouro: "",
            complemento: "",
            bairro: "",
            cidade: "",
            uf: "",
            ddd: "",
            isValid: false,
        };
    },
    methods: {
        //https://viacep.com.br/ws/65631375/json/
       async searchCep() {
           try {
               const response = await api.get(`${this.cepSearch}/json`);
               const data = await response.data;
               //console.log(data);
               this.isValid = true;
               if(data.erro === true){
                   alert("Cep não encontrado!");
               }else{
                    this.cep = data.cep;
                    this.logradouro = data.logradouro;
                    if(data.complemento === ""){
                            this.complemento = "Não informado";
                    }else{
                        this.complemento = data.complemento;
                    }   
                    this.bairro = data.bairro;
                    this.cidade = data.localidade;
                    this.uf = data.uf;
                    this.ddd = data.ddd;

                
               }
            } catch (error) {
                alert("CEP não encontrado");
                this.cepSearch = "";
            }
               
           
        },
    },

}

</script>

<style scoped>
.container {
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: rgb(2,0,36);
    background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(9,9,121,1) 41%, rgba(0,212,255,1) 100%);

}
.title {
    color: #fff;
    font-size: 4rem;
    font-weight: bold;
    margin-bottom: 1rem;
    animation: flipTitle 1s;
}

@keyframes flipTitle {
    from {
        transform: rotateX(90deg);
    }
    to {
        transform: rotateX(0deg);
    }
}

.containerInput {
    background-color: rgba(255,255,255,0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 15px;
    margin:30px 0;
    border-radius: 8px;
}

.containerInput input {
    background-color: transparent;
    color: #fff;
    border: none;
    font-size: 1.5rem;
    outline: none;
    margin-right: 0.5rem;
}

.searchButton{
    background-color: transparent;
    border: none;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    transition: 0.3s;
    color: #fff;
}

.searchButton:hover {
    transform: scale(1.3);
}

.main{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 8px;
    width: 400px;
    color: #fff;
}

.main h2{
    margin: 16px 8px;
    font-size: 1.5rem;
    color: #fff;
}

.main span{
    margin-bottom: 16px;
    font-weight: bold;
}
.main strong{
    color: #41B883;
}

@media(max-width: 400px) {
    .container{
        width: auto;
    }
    
    .containerInput{
        width: 80%;
    }
    
    .title{
        font-size:60px;
    }
    .main{
        width: 80%;
    }
    .main h2{
        font-size:24px;
    }
}
</style>