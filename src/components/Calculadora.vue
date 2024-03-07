<script setup>
import { reactive } from 'vue';

const estado = reactive({
    numero1: 0,
    numero2: 0,
    operacoes: {
        somar: (x, y) => x + y,
        subtrair: (x,y) => x - y,
        multiplicar: (x, y) => x * y,
        dividir: (x,y) => (y !== 0 ? x / y : 'Tente outro numero, essa é uma divisão por ZERO'),
    },
    resultado: '',
})

const calcResultado = () => {
    const { numero1, numero2, operacao } = estado;
    if (!isNaN(parseFloat(numero1 && numero2)) && isFinite(numero1 && numero2)){
        estado.resultado = estado.operacoes[operacao](parseFloat(numero1), parseFloat(numero2));
    } else {
        estado.resultado = '';
    }
};

</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-dark text-warning rounded-5">
        <h1 class="text-center">Calculadora Aritmética</h1>
        <p v-if="estado.resultado === ''" class="mt-4 fs-3 text-light">
            O resultado é: 
        </p>
        
        <p v-else class="mt-4 fs-3 text-light">
            O resultado é: {{  estado.resultado }}
        </p>
    </header>
    <form>
        <input type="number" v-model="estado.numero1" @input="calcResultado" min="0" required placeholder="Informe um numero" class="form-control mb-3">
        <select v-model="estado.operacao" @change="calcResultado" class="form-control mb-3">
            <option value="somar">Somar</option>
            <option value="subtrair">Subtrair</option>
            <option value="multiplicar">Multiplicar</option>
            <option value="dividir">Dividir</option>
        </select>
        <input type="number" v-model="estado.numero2" @input="calcResultado" min="0" required placeholder="Informe um numero" class="form-control ">
    </form>
</template>