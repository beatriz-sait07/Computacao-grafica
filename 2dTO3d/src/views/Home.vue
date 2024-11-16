<template>
    <!-- <div id="apresentação" class="absoluted w-full h-screen flex flex-col items-center justify-center">
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
                    class="bg-gray-700 px-12 py-2 rounded-full shadow-slate-700 shadow-xl cursor-pointer">
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
    </div> -->

    <div id="visualOpcoes" class="flex absoluted w-full h-screen flex-col items-center justify-center">
        <header class="w-full h-[20%] text-xl text-center flex flex-col p-2">
            <button id="close"
                class="relative mt-2 bg-red-900 px-3 py-2 rounded-full cursor-pointer self-end italic">X</button>
            <p class="relative text-md font-black p-2">Projeto conversão de imagem 2D para 3D</p>
        </header>

        <div id="fotoTirada" class="flex flex-col justify-center border-1 w-[90%] h-[60%] ">
            <button id="takeFoto"
                class="flex gap-2 bg-gray-700 rounded-full w-36 h-10 justify-center items-center font-black">
                <svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none"
                    viewBox="0 0 24 24">
                    <path stroke="currentColor" stroke-linejoin="round" stroke-width="2"
                        d="M4 18V8a1 1 0 0 1 1-1h1.5l1.707-1.707A1 1 0 0 1 8.914 5h6.172a1 1 0 0 1 .707.293L17.5 7H19a1 1 0 0 1 1 1v10a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1Z" />
                    <path stroke="currentColor" stroke-linejoin="round" stroke-width="2"
                        d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" />
                </svg>
                Tirar Foto
            </button> <!--tira a foto meio obvio-->

            <section id="sendImg"
                class="flex bg-gray-700 w-full h-[60%] md:h-[85%] rounded-xl  justify-center items-center">
                <video id="preparaTirarFoto" class="w-[60%] h-[80%] flex object-fill" autoplay></video>
                <!--onde a img vai aparece/ autoplay not is obrigation-->
                <canvas id="rendFoto" class="w-[60%] h-[80%] hidden object-fill"></canvas>
                <!-- rederiza a img -->
            </section>
        </div>

        <footer class="w-full h-[10%] flex flex-col justify-center items-center p-6 text-center gap-2 text-sm">
            <ul class="flex gap-6">
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


function enviarFoto() {
    var video = document.querySelector('#preparaTirarFoto');

    const specs = {
        video: {
            with: 320,
            height: 110,
        }
    }

    navigator.mediaDevices.getUserMedia(specs)
        .then(stream => {
            video.srcObject = stream; //pegando frames do video 
            video.play(); // "vendo video"
        })
        .catch(e => {
            console.error('Erro', e)
        })
}

function confirmAcction(element) {
    $(element).append(`
        <div id="submitFotoTirada" class="hidden w-full h-[10%] justify-center gap-3 items-center">
            <button id="confirSend"
                class="relative mt-2 bg-green-900 w-[40%] h-[24px] rounded-full cursor-pointer self-end italic">Salvar</button>
            <button id="cancelSend"
                class="relative mt-2 bg-red-900 w-[40%] h-[24px] rounded-full cursor-pointer self-end italic">Cancelar</button>
        </div>
    `)
}

//-------JQUERY question-------
$(document).ready(function () {
    $("#opc").click(function () {
        $('#iniciarApp1').append(`
            <div class="opcoes">
                <lu class="flex gap-5 ">
                    <li id="anexo" class="bg-gray-800 rounded-full p-2 cursor-pointer">Anexar Foto</li>
                    <li id="busca" class="bg-gray-800 rounded-full p-2 cursor-pointer">Buscar Foto</li>
                    <li id="tirar" class="bg-gray-800 rounded-full p-2 cursor-pointer">Tirar Foto</li>
                </lu>
            </div>
        `)

        $("#tirar").click(function () {
            console.log('funfou2');
            $('#apresentação').removeClass('flex').addClass('hidden');
            $('#visualOpcoes').removeClass('hidden').addClass('flex');
            $('#fotoTirada').removeClass('hidden').addClass('flex');
        })


    });

    $('#close').click(function () {
        console.log('feche nengue');
        $('#visualOpcoes').removeClass('flex').addClass('hidden');
        $('#apresentação').removeClass('hidden').addClass('flex')


    })

    $('#takeFoto').click(function () {
        enviarFoto()
        $('#takeFoto').removeClass('flex').addClass('hidden');
        $('#submitFotoTirada').removeClass('hidden').addClass('flex');
        confirmAcction('#sendImg')
    })


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
