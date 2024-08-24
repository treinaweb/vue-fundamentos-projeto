<script setup>
const props = defineProps({
    produto: {
        type: Object,
        required: true,
    },
});
</script>

<template>
    <div class="product-card">
        <img
            :src="produto.imagem"
            alt="Imagem do produto"
            width="100%"
            height="183px"
        />
        <h3>{{ produto.nome }}</h3>
        <p>{{ produto.descricao }}</p>
        <span>${{ produto.preco.toFixed(2) }}</span>
    </div>
</template>

<style scoped>
.product-card {
    border: 1px solid #ddd;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;
}

.product-card h3 {
    color: #fff;
    font-weight: 600;
}

.product-card span {
    color: green;
}
</style>
