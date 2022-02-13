<template>
    <div class="container">
        <h1 class="title">SEU CEP</h1>
        <div class="containerInput">
            <input type="text" v-model="cep" placeholder="Digite seu Cep..." />
            <button @click="searchCep" class="searchButton">
                <Search :size="28" class="searchIcon"/>
            </button>
        </div>

        <main class="main">
            <h2>Seu Cep: 65631-375</h2>
            <span>Rua: Rua dos Bobos</span>
            <span>Complemento: Alguma coisa</span>
            <span>Bairro: Centro</span>
            <span>Cidade: Timon UF: MA</span>
        </main>
    </div>
</template>

<script>
import Search from "vue-material-design-icons/Magnify";
export default {
    name: "SearchCep",
    components: {
        Search,
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
}

.searchButton:hover {
    transform: scale(1.2);
}
</style>