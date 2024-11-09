<template>
    <header class="w-full h-[10%] text-2xl text-center flex items-center justify-center">
        <p>Projeto conversão de imagem 2D para 3D</p>
    </header>

    <body class="w-full h-[80%] bg-blue-500">
        <section class="carroselImgInicial bg-red-100 w-full h-[80%] flex flex-row justify-center items-center">
            <img class="w-[900px] " src="../assets/carrossel/img1.png" alt="">
            <img class="w-[600px] " src=" ../assets/carrossel/img2.png" alt="">
            <!-- <img class="w-[900px] " src=" ../assets/carrossel/img3.png" alt=""> -->
        </section>
    </body>
    <footer class="w-full h-[10%] bg-blue-800 text-white flex flex-col justify-center items-center ">
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