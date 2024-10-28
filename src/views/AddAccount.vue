<template>
    <main class="acc">
        <h1>Kelola Akun</h1>
        <p>Tambah/Hapus Akun</p>
    </main>
</template>

<script setup>

</script>

<style lang="scss" scoped>
main {
    padding: 1.4rem;
    h1 {
        color: var(--green-kkc);
        font-weight: 700;
    }
}

.cards-wrapper {
    display: flex;
    gap: 0.9rem; /* Memberikan jarak antar card */
    padding: 1.4rem;
}

.card-op, .card-non-op, .card-prive {
    display: flex;
    flex-direction: column; /* Menjaga konten card tetap vertikal */
    padding: 1.4rem;
}
</style>
