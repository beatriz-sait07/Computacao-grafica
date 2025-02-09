<template>
    <div id="apresentação" class="absoluted w-full h-screen flex flex-col items-center justify-center">
        <header class="w-full h-[5%] text-2xl text-center flex items-center justify-center md:text-4xl fixed">
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
                    class="bg-transparent px-12 py-2 rounded-full shadow-slate-700 shadow-lg cursor-pointer border-2 border-gray-500">
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

    <div id="visualOpcoes" class="hidden absoluted w-full h-screen flex-col items-center">
        <div class="w-full h-[20%] text-xl text-center flex flex-col p-2">
            <button id="close"
                class="relative mt-2 bg-red-900 px-3 py-2 rounded-full cursor-pointer self-end italic">X</button>
            <p class="relative text-md font-black p-2">Projeto conversão de imagem 2D para 3D</p>
        </div>

        <div id="fotoTirada" class="hidden flex-col justify-center border-1 w-[90%] h-[60%] md:w-[60%]">
            <section id="sendImg"
                class="flex bg-gray-700 w-full h-[60%] md:h-[85%] rounded-xl justify-center items-center flex-col gap-2 p-2">
                <video id="preparaTirarFoto" class="w-[50%] h-[80%] flex object-fill" autoplay></video>
                <canvas id="rendFoto" class="w-[60%] h-[80%] hidden object-fill"></canvas>
                <button id="takeFoto"
                    class="flex gap-2 bg-gray-800 rounded-full w-36 h-10 justify-center items-center font-black">
                    <svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none"
                        viewBox="0 0 24 24">
                        <path stroke="currentColor" stroke-linejoin="round" stroke-width="2"
                            d="M4 18V8a1 1 0 0 1 1-1h1.5l1.707-1.707A1 1 0 0 1 8.914 5h6.172a1 1 0 0 1 .707.293L17.5 7H19a1 1 0 0 1 1 1v10a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1Z" />
                        <path stroke="currentColor" stroke-linejoin="round" stroke-width="2"
                            d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z" />
                    </svg>
                    Tirar Foto
                </button>
            </section>
        </div>
        <div id="buscarFotoBanco"
            class="hidden flex-col justify-around items-center border-1 w-[90%] h-[60%] md:w-[60%] bg-transparent rounded-lg p-2">
            <section class="w-full flex justify-center">
                <div class="w-[80%] rounded-lg border-2 bg-transparent border-gray-500 flex px-3 py-1">
                    <input type="text" name="buscaImg" id="buscaImg" class="bg-transparent flex-1">
                    <svg class="w-6 h-6 text-gray-500" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24"
                        height="24" fill="none" viewBox="0 0 24 24">
                        <path stroke="currentColor" stroke-linecap="round" stroke-width="2"
                            d="m21 21-3.5-3.5M17 10a7 7 0 1 1-14 0 7 7 0 0 1 14 0Z" />
                    </svg>

                </div>
            </section>
            <section class="w-full flex justify-center h-[60%]">
                <!--botar um loader para mostra a busca-->
                <div class="w-[80%] h-full rounded-lg border-2 bg-transparent border-gray-500 flex p-2">
                    <p>busca do banco</p>
                </div>
            </section>
        </div>

        <!-- <div id="anexarFoto"
            class="hidden flex-col justify-around items-center border-2 border-gray-500 w-[90%] h-[60%] md:w-[60%] rounded-lg p-2">
            <form action="caminho.back" method="post" enctype="multipart/form-data" class="w-full h-full flex flex-col">
                <h1 class="w-full h-[15%] flex justify-center items-center text-2xl">Anexar arquivos da galeria</h1>
                <div
                    class="w-full flex-1 border border-gray-400 rounded-md hover:bg-slate-800 hover:rounded-md hover:font-black">
                    <label class="w-full h-full cursor-pointer flex justify-center items-center " for="arq">Anexar
                        imagem
                        a ser
                        convertida</label>
                    <input class="hidden" type="file" name="arquivo2d" id="arq" accept="image/*">
                </div>
                <div id="preview-container" class="w-full h-[50%] flex justify-center items-center mt-4">
                    <img id="preview-image" class="hidden max-w-full max-h-full border border-gray-300 rounded-lg"
                        alt="Pré-visualização da imagem">
                </div>
                <div class="w-full h-[20%] flex justify-center items-center">
                    <button
                        class="w-[90%] md:w-[60%] text-sm font-medium border border-gray-400 rounded-md p-2 hover:bg-slate-800 hover:rounded-md hover:font-black"
                        type="submit">
                        Visualizar imagem em 3D
                    </button>
                </div>
            </form>
        </div> -->
        <div id="anexarFoto"
            class="hidden flex-col justify-around items-center border-2 border-gray-500 w-[90%] h-[60%] md:w-[60%] rounded-lg p-2">
            <form @submit.prevent="enviarImagem" class="w-full h-full flex flex-col">
                <h1 class="w-full h-[15%] flex justify-center items-center text-2xl">Anexar arquivos da galeria</h1>
                <div
                    class="w-full flex-1 border border-gray-400 rounded-md hover:bg-slate-800 hover:rounded-md hover:font-black">
                    <label class="w-full h-full cursor-pointer flex justify-center items-center" for="arq">Anexar imagem
                        a ser convertida</label>
                    <input class="hidden" type="file" name="arquivo2d" id="arq" accept="image/*"
                        @change="handleFileChange">
                </div>
                <div id="preview-container" class="w-full h-[50%] flex justify-center items-center mt-4">
                    <img id="preview-image" class="hidden max-w-full max-h-full border border-gray-300 rounded-lg"
                        alt="Pré-visualização da imagem">
                </div>
                <div class="w-full h-[20%] flex justify-center items-center">
                    <button
                        class="w-[90%] md:w-[60%] text-sm font-medium border border-gray-400 rounded-md p-2 hover:bg-slate-800 hover:rounded-md hover:font-black"
                        type="submit">
                        Visualizar imagem em 3D
                    </button>
                </div>
            </form>
        </div>

        <div id="exibirObj" class="hidden w-[80%] justify-center rounded-md">
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';
import $ from 'jquery';
import { Scene, PerspectiveCamera, WebGLRenderer, DirectionalLight, AmbientLight, BoxGeometry, MeshBasicMaterial, Mesh } from 'three';
import { OBJLoader } from 'three/examples/jsm/loaders/OBJLoader.js';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';

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
    const containerRender = document.getElementById('exibirObj');

    if (!containerRender) {
        console.error("Conteiner 'exibirObj' não encontrado.");
        return;
    }

    const width = containerRender.clientWidth || window.innerWidth;
    const height = containerRender.clientHeight || window.innerHeight;

    const render = new WebGLRenderer({ alpha: true });
    render.setClearColor(0x000000, 0); // Fundo transparente
    render.clear();
    render.setSize(width, height);
    containerRender.appendChild(render.domElement);

    // Criando cena e câmera
    const cena = new Scene();
    const camera = new PerspectiveCamera(75, width / height, 0.1, 1000);
    camera.position.set(0, 1, 5);

    // Adicionando luzes
    const luzDirecional = new DirectionalLight(0xffffff, 1);
    luzDirecional.position.set(1, 1, 1).normalize();
    cena.add(luzDirecional);

    const luzAmbiente = new AmbientLight(0x404040);
    cena.add(luzAmbiente);

    const controls = new OrbitControls(camera, render.domElement);
    controls.enableDamping = true;
    controls.dampingFactor = 0.05;
    controls.enableZoom = true;

    // Carregando objeto 3D
    const loader = new OBJLoader();
    loader.setPath('../src/assets/');
    loader.load(
        'teste01.obj',
        (obj) => {
            obj.scale.set(1, 1, 1);
            obj.position.set(0, 0, 0);
            cena.add(obj);
            console.log('Objeto carregado com sucesso!');
        },
        (progress) => console.log(`Carregando: ${(progress.loaded / progress.total) * 100}%`),
        (error) => console.error('Erro ao carregar o objeto:', error)
    );

    // Função de animação
    const animate = () => {
        controls.update();
        render.render(cena, camera);
        requestAnimationFrame(animate);
    };

    animate();
});

//FUNCOES DE FUNCIONAMENTO DE CLICK E AFINS
onMounted(() => {
    setInterval(slide, 3000);
});

function enviarFotoTirada() {
    var video = document.querySelector('#preparaTirarFoto');

    const specs = {
        video: {
            with: 320,
            height: 110,
        }
    }
    navigator.mediaDevices.getUserMedia(specs)
        .then(stream => {
            video.srcObject = stream;
            video.play();
        })
        .catch(e => {
            console.error('Erro', e)
        })
}

function desligarCamera() {
    var video = document.querySelector('#preparaTirarFoto');

    if (video.srcObject) {
        video.srcObject.getTracks().forEach(track => {
            track.stop();
        });
        video.srcObject = null;
    }
    fecharOpc()
}
function fecharOpc() {
    $('#visualOpcoes').on('click', '#close', function () {
        console.log('feche nengue');
        if ($('#visualOpcoes').length === 0) $('#apresentação').toggleClass('hidden flex');

        $('#visualOpcoes').removeClass('flex').addClass('hidden');
        $('#apresentação').removeClass('hidden').addClass('flex');;
        $('#fotoTirada').removeClass('flex').addClass('hidden');
        $('#buscarFotoBanco').removeClass('flex').addClass('hidden');
        $('#anexarFoto').removeClass('flex').addClass('hidden');
        $('#exibirObj').removeClass('flex').addClass('hidden');
        desligarCamera()
    })
}

function confirmAcction(element) {
    $(element).append(`
        <div id="submitFotoTirada" class="flex w-full h-[10%] justify-center gap-3 items-center">
            <button id="confirSend"
                class="relative mt-2 bg-green-900 w-[40%] h-[24px] rounded-full cursor-pointer self-end italic">Salvar</button>
            <button id="cancelSend"
                class="relative mt-2 bg-red-900 w-[40%] h-[24px] rounded-full cursor-pointer self-end italic">Cancelar</button>
        </div>
    `);

    // Evento para confirmar
    $('#fotoTirada').on('click', '#confirSend', async function () {
        desligarCamera();
        $('#fotoTirada').toggleClass('hidden flex');
        $('#exibirObj').toggleClass('hidden flex');
        $('#sendFoto').removeClass('hidden');
        await enviarFotoParaBackend(); // Chama a função correta
    });

    $('#fotoTirada').on('click', '#cancelSend', function () {
        $(element).find('canvas').removeClass('flex').addClass('hidden');
        $(element).find('video').removeClass('hidden').addClass('flex');
        enviarFotoTirada();
        desligarCamera();
    });
}

onMounted(() => {
    const fileInput = document.getElementById('arq');
    const previewImage = document.getElementById('preview-image');
    const previewContainer = document.getElementById('preview-container');

    if (fileInput) {
        fileInput.addEventListener('change', function (event) {
            const file = event.target.files[0];

            if (file && file.type.startsWith('image/')) {
                const reader = new FileReader();

                reader.onload = function (e) {
                    previewImage.src = e.target.result;
                    previewImage.classList.remove('hidden');
                };

                reader.readAsDataURL(file);
            } else {
                previewImage.classList.add('hidden');
            }
        });
    } else console.error("Elemento 'fileInput' não encontrado no DOM.");

});

//-------JQUERY question-------
$(document).ready(function () {
    $('#iniciarApp1').on('click', '#opc', function () {
        if ($('.opcoes').length === 0) {
            $('#iniciarApp1').append(`
                <div class="opcoes">
                    <lu class="flex gap-5 ">
                        <li id="anexo" class="bg-transparent border-2 border-gray-500 rounded-full p-4 cursor-pointer">Anexar Foto</li>
                        <li id="busca" class="bg-transparent border-2 border-gray-500 rounded-full p-4 cursor-pointer">Buscar Foto</li>
                        <li id="tirar" class="bg-transparent border-2 border-gray-500 rounded-full p-4 cursor-pointer">Tirar Foto</li>
                    </lu>
                </div>
            `);
        } else $('.opcoes').toggleClass('hidden flex');


        $('#apresentação').on('click', '#tirar', function () {
            $('#apresentação').toggleClass('flex hidden');
            $('#visualOpcoes').toggleClass('hidden flex');
            $('#fotoTirada').toggleClass('hidden flex');
            enviarFotoTirada()

            $('#visualOpcoes').on('click', '#takeFoto', function () {
                console.log('tentou tirar')
                var video = $('#preparaTirarFoto')[0];
                var canvas = $('#rendFoto')[0];
                var context = canvas.getContext('2d');

                canvas.width = video.videoWidth;
                canvas.height = video.videoHeight;

                context.drawImage(video, 0, 0, canvas.width, canvas.height);

                $('#takeFoto').toggleClass('hidden flex');
                $('#preparaTirarFoto').toggleClass('hidden flex');
                $('#rendFoto').toggleClass('hidden flex');
                confirmAcction('#fotoTirada');
            });
        });

        $('#apresentação').on('click', '#busca', function () {
            $('#fotoTirada').addClass('hidden');
            $('#apresentação').removeClass('flex').addClass('hidden');
            $('#visualOpcoes').removeClass('hidden').addClass('flex');
            $('#buscarFotoBanco').removeClass('hidden').addClass('flex');

        })

        $('#apresentação').on('click', '#anexo', function () {
            console.log('Anexar Foto clicado!');
            $('#apresentação').toggleClass('flex hidden');
            $('#visualOpcoes').toggleClass('hidden flex');
            $('#anexarFoto').toggleClass('hidden flex');
        });

    });

    fecharOpc()

});

function processarMatriz(matriz) {
    // Exemplo de processamento da matriz, você pode ajustar conforme a estrutura exata
    const vertices = [];
    const linhas = matriz.split("\n");

    for (let linha of linhas) {
        if (linha.startsWith('v')) {
            const valores = linha.split(' ').slice(1); // Remove o 'v' e pega os valores
            const coordenadas = valores.map(parseFloat); // Converte para float
            vertices.push(coordenadas);
        }
    }

    return vertices;
}

function renderizarMatriz3D(vertices) {
    const containerRender = document.getElementById('exibirObj');
    const width = containerRender.clientWidth || window.innerWidth;
    const height = containerRender.clientHeight || window.innerHeight;

    const renderer = new WebGLRenderer({ alpha: true });
    renderer.setSize(width, height);
    containerRender.appendChild(renderer.domElement);

    const scene = new Scene();
    const camera = new PerspectiveCamera(75, width / height, 0.1, 1000);
    camera.position.set(0, 1, 5);

    const light = new DirectionalLight(0xffffff, 1);
    light.position.set(1, 1, 1).normalize();
    scene.add(light);

    const geometry = new Geometry();
    vertices.forEach(vertex => {
        geometry.vertices.push(new Vector3(vertex[0], vertex[1], vertex[2]));
    });

    const material = new PointsMaterial({ color: 0x00ff00, size: 0.1 });
    const points = new Points(geometry, material);
    scene.add(points);

    const controls = new OrbitControls(camera, renderer.domElement);
    controls.enableZoom = true;

    function animate() {
        controls.update();
        renderer.render(scene, camera);
        requestAnimationFrame(animate);
    }

    animate();
}

async function processarResposta(response) {
    try {
        // Supondo que a resposta seja uma string de coordenadas ou dados de vértices
        const vertices = processarMatriz(response.matriz); // Aqui você usa a função de processamento de matriz

        // Chama a função de renderização para gerar o objeto 3D
        renderizarMatriz3D(vertices);
    } catch (error) {
        console.error("Erro ao processar a resposta:", error);
    }
}

const enviarFotoBack = async () => {
    try {
        // Primeiro, verifica se o arquivo de imagem foi selecionado
        if (!image) {
            alert('Por favor, selecione uma imagem.');
            return;
        }

        // Agora, envia a imagem ao backend
        const formData = new FormData();
        formData.append('image', image);

        // Substitua a URL pela URL da sua API de envio
        const response = await fetch('https://5c34-35-231-79-166.ngrok-free.app/pifuhd', {
            method: 'POST',
            body: formData,
        });

        const data = await response.json();

        if (response.ok) {
            alert('Imagem enviada com sucesso!');
            processarResposta(data);
        } else {
            alert('Erro ao enviar a imagem: ' + data.message);
        }
    } catch (error) {
        console.error("Erro ao enviar a foto:", error);
    }
};


function handleFileChange(event) {
    const file = event.target.files[0];
    const previewImage = document.getElementById('preview-image');

    if (file && file.type.startsWith('image/')) {
        const reader = new FileReader();
        reader.onload = function (e) {
            previewImage.src = e.target.result;
            previewImage.classList.remove('hidden');
        };
        reader.readAsDataURL(file);
    } else {
        previewImage.classList.add('hidden');
    }
}


async function enviarFotoParaBackend() {
    var canvas = document.getElementById('rendFoto');
    var imageData = canvas.toDataURL("image/jpeg"); // Captura a imagem do canvas como Base64

    // Converte Base64 para Blob
    const byteString = atob(imageData.split(',')[1]); // Remove a parte 'data:image/png;base64,'
    const arrayBuffer = new ArrayBuffer(byteString.length);
    const uint8Array = new Uint8Array(arrayBuffer);

    for (let i = 0; i < byteString.length; i++) {
        uint8Array[i] = byteString.charCodeAt(i);
    }

    const blob = new Blob([uint8Array], { type: 'image/jpeg' });

    // Adiciona o Blob ao FormData
    const formData = new FormData();
    formData.append('image', blob, 'canvas-image.jpeg');

    // Envia para o backend
    await fetch("https://5c34-35-231-79-166.ngrok-free.app/pifuhd", {
        method: 'POST',
        body: formData,
    })
        .then(response => {
            if (!response.ok) {
                throw new Error(`Erro na resposta: ${response.statusText}`);
            }
            return response.blob();
        })
        .then(blob => {
            const objectUrl = URL.createObjectURL(blob);
            console.log("OBJ File URL:", objectUrl);
            const link = document.createElement('a');
        })
        .catch(error => console.error('Erro ao enviar foto para backend:', error));
}
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

.c-loader {
    width: 80px;
    height: 80px;
    border: 5px solid #D9D9D9;
    border-radius: 100%;
    border-top-color: #333333;
    animation: isRotating 1s infinite;
}

@keyframes isRotating {
    to {
        transform: rotate(1turn);
    }
}
</style>
