<template>
    <main class="input-transac-page">
        <h1>Pengaturan</h1>
        <!-- <p>Halaman Catat Pengeluaran</p> -->
    </main>
    <div class="card">
        <AccManagerCard/>
    </div>

</template>

<script setup>
import AccManagerCard from '../components/AccManagerCard.vue';
</script>

<style lang="scss" scoped>
 main{
    padding: 1.4rem;
    h1{
        color: var(--green-kkc);
        font-weight: 700;
    }
 }

 .card{
    padding: 1.4rem;
 }
</style>