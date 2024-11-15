<template>
    <header class="w-full h-[5%] text-2xl text-center flex items-center justify-center md:text-4xl">
        <p class="relative mt-10">Projeto conversão de imagem 2D para 3D</p>
    </header>
    <div class="w-full h-[85%] flex flex-col justify-center items-center">
        <section class="carroselImgInicial w-full h-[80%] flex flex-row justify-center items-center">
            <img class="w-[200px]" src=" ../assets/carrossel/img1.png" alt="">
            <img class="w-[200px] " src=" ../assets/carrossel/img2.png" alt="">
            <img class="w-[200px] " src=" ../assets/carrossel/img3.png" alt="">
        </section>
        <article class="h-[18%] w-full  flex justify-center items-center">
            <button class="">
                Iniciar
            </button>
        </article>
    </div>
    <footer class="w-full h-[10%] flex flex-col justify-center items-center ">
        <lu class="flex gap-3">
            <li>Beatriz Saito </li>
            <li>Maria Angélica</li>
            <li>Taynan Mancilla</li>
        </lu>
        <p>&copy; 2024</p>
    </footer>
</template>

<script>
import $ from 'jquery'


</script>

<style>
li {
    list-style-type: none;
}

.flex {
    display: flex;
    gap: 0.5rem;
    list-style: none;
    padding: 0;
    margin: 0;
}

.flex li::after {
    content: "|";
    margin-left: 0.5rem;
    color: white;
}

.flex li:last-child::after {
    content: "";
}
</style>