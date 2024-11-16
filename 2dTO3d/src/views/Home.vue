<template>
    <div id="apresentação" class="absoluted w-full h-screen flex flex-col items-center justify-center">
        <header class="w-full h-[5%] text-2xl text-center flex items-center justify-center md:text-4xl">
            <p class="relative mt-16">Projeto conversão de imagem 2D para 3D</p>
        </header>

        <div class=" w-full h-[85%] flex flex-col justify-center items-center">
            <section class="carroselContainer h-[60%] flex overflow-hidden relative">
                <div v-for="(img, index) in imagens" :key="index" :class="[
                    'carrosselItem',
                    { active: index === indexAtual, left: index === leftIndex, right: index === rightIndex }
                ]">
                    <img :src="img.src" :alt="img.alt" />
                </div>
            </section>
            <article id="iniciarApp1" class="h-[35%] w-full flex justify-center items-center flex-col-reverse gap-3">
                <button id="opc" @click="iniciarApp"
                    class="bg-gray-700 px-12 py-2 rounded-full shadow-slate-700 shadow-xl">
                    Iniciar
                </button>
            </article>
        </div>
        <footer class="w-full h-[10%] flex flex-col justify-center items-center p-6 text-center gap-2 text-sm">
            <ul class="flex gap-6 ">
                <li class="liFoot underline underline-offset-2">Beatriz Saito</li>
                <li class="liFoot underline underline-offset-2">Maria Angélica</li>
                <li class="liFoot underline underline-offset-2">Taynan Mancilla</li>
            </ul>
            <p class="text-white">&copy; 2024</p>
        </footer>
    </div>
    <div id="visualOpcoes" class="hidden absoluted w-full h-screen flex-col items-center justify-center">
        <header class="w-full h-[5%] text-2xl text-center flex items-center justify-center md:text-4xl">
            <p class="relative mt-16">Projeto conversão de imagem 2D para 3D</p>
            <p class="relative mt-2 bg-red-900">X</p>
        </header>

        <div class=" w-full h-[85%] flex flex-col justify-center items-center">
            
        </div>
        <footer class="w-full h-[10%] flex flex-col justify-center items-center p-6 text-center gap-2 text-sm">
            <ul class="flex gap-6 ">
                <li class="liFoot underline underline-offset-2">Beatriz Saito</li>
                <li class="liFoot underline underline-offset-2">Maria Angélica</li>
                <li class="liFoot underline underline-offset-2">Taynan Mancilla</li>
            </ul>
            <p class="text-white">&copy; 2024</p>
        </footer>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import $ from 'jquery';

const imagens = ref([
    { src: "../src/assets/carrossel/img1.png", alt: "CADERNO" },
    { src: "../src/assets/carrossel/img2.png", alt: "CIFRAO" },
    { src: "../src/assets/carrossel/img3.png", alt: "PICOLE MORDIDO" },
]);
const indexAtual = ref(0);
const slide = () => {
    indexAtual.value = (indexAtual.value + 1) % imagens.value.length;
};
const leftIndex = computed(() => {
    return (indexAtual.value - 1 + imagens.value.length) % imagens.value.length;
});
const rightIndex = computed(() => {
    return (indexAtual.value + 1) % imagens.value.length;
});

onMounted(() => {
    setInterval(slide, 3000);
});

//-------JQUERY question-------
$(document).ready(function () {
    $("#opc").click(function () {
        $('#iniciarApp1').append(`
            <div class="opcoes">
                <lu class="flex gap-5">
                    <li id="anexo" class="bg-gray-800 rounded-full p-2">Anexar Foto</li>
                    <li id="busca" class="bg-gray-800 rounded-full p-2">Buscar Foto</li>
                    <li id="tirar" class="bg-gray-800 rounded-full p-2">Tirar Foto</li>
                </lu>
            </div>
        `)

        $("#tirar").click(function () {
            console.log('funfou2');
            $('#apresentação').removeClass('flex').addClass('hidden');
            $('#visualOpcoes').removeClass('hidden').addClass('flex');
        })
    });
});


</script>

<style>
.carroselContainer {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 600px;
    height: 100%;
    position: relative;
}

.carrosselItem {
    position: absolute;
    opacity: 0.5;
    transition: transform 0.5s ease, opacity 0.5s ease, z-index 0.5s;
    transform: scale(0.8);
    z-index: 1;
}

.carrosselItem.active {
    transform: scale(1);
    opacity: 1;
    z-index: 3;
}

.carrosselItem.left {
    transform: translateX(-150px) scale(0.7);
    z-index: 2;
    opacity: 0.5;
}

.carrosselItem.right {
    transform: translateX(150px) scale(0.7);
    z-index: 2;
    opacity: 0.5;
}

.carrosselItem img {
    width: 200px;
    height: auto;
    border-radius: 10px;
}

li {
    list-style-type: none;
}
</style>
