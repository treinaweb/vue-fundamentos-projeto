<!-- src/App.vue -->
<script setup>
import { ref } from "vue";
import ProductCard from "./components/ProductCard.vue";

// Dados de exemplo
const produtos = ref([
    {
        id: 1,
        nome: "Pizza Calabresa",
        descricao: "Pizza com calabresa, cebola e azeitonas.",
        preco: 29.99,
        imagem: "https://www.sabornamesa.com.br/media/k2/items/cache/513d7a0ab11e38f7bd117d760146fed3_XL.jpg",
    },
    {
        id: 2,
        nome: "Pizza 4 Queijos",
        descricao: "Pizza com mussarela, parmesão, provolone e gorgonzola.",
        preco: 34.99,
        imagem: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTAyPQB4_wzkNfqFG8mRV9usgW78Y-So92M8A&s",
    },
    {
        id: 3,
        nome: "Pizza Margherita",
        descricao: "Pizza com mussarela, tomate, manjericão e azeite.",
        preco: 32.99,
        imagem: "https://www.sabornamesa.com.br/media/k2/items/cache/2c3125eb8597b442fad87e2c031423e6_XL.jpg",
    },
]);

// Dados do novo produto
const novoProduto = ref({
    nome: "",
    descricao: "",
    preco: 0,
    imagem: "",
});

// Função para adicionar um novo produto
function adicionarProduto() {
    produtos.value.push({
        id: produtos.value.length + 1, // Simples incremento para ID
        ...novoProduto.value,
    });

    // Limpar o formulário
    novoProduto.value = {
        nome: "",
        descricao: "",
        preco: 0,
        imagem: "",
    };
}
</script>
<template>
    <div>
        <h1>Catálogo de Produtos</h1>

        <!-- Formulário para adicionar novos produtos -->
        <form @submit.prevent="adicionarProduto">
            <div>
                <label for="nome">Nome:</label>
                <input
                    v-model="novoProduto.nome"
                    id="nome"
                    type="text"
                    required
                />
            </div>
            <div>
                <label for="descricao">Descrição:</label>
                <input
                    v-model="novoProduto.descricao"
                    id="descricao"
                    type="text"
                    required
                />
            </div>
            <div>
                <label for="preco">Preço:</label>
                <input
                    v-model.number="novoProduto.preco"
                    id="preco"
                    type="number"
                    step="0.01"
                    required
                />
            </div>
            <div>
                <label for="imagem">Imagem URL:</label>
                <input
                    v-model="novoProduto.imagem"
                    id="imagem"
                    type="text"
                    required
                />
            </div>
            <button type="submit">Adicionar Produto</button>
        </form>

        <!-- Lista de produtos -->
        <div class="product-list">
            <ProductCard
                v-for="produto in produtos"
                :key="produto.id"
                :produto="produto"
            />
        </div>
    </div>
</template>

<style scoped>
.product-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
    margin-top: 1rem;
}

form {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

form label {
    display: block;
    margin-bottom: 0.2rem;
}

form input {
    width: 100%;
    padding: 0.5rem;
    box-sizing: border-box;
}

button {
    padding: 0.5rem 1rem;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    max-width: 200px;
    margin-left: auto;
}

button:hover {
    background-color: #0056b3;
}
</style>
