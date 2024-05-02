<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">BUKU</h2>
                <form @submit.prevent="getBUKU">
                    <input v-model="keyword" type="search" class="form-control rounded-5">
                </form>
                <div class="my-3 text-muted">menampilkan 3 dart 3</div>
                <div v-for="(BUKU,i) in BUKU" :key="i" class="col-lg-2">
                    <div class="card mb-3">
                        <div class="card-body">
                            <img :src="BUKU.cover" class="cover" alt="cover">
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <NuxtLink to="/">
            <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">kembali</button>
        </NuxtLink>
    </div>
</template>
<script setup>
const keyword = ref('')

const supabase = useSupabaseClient()

const BUKU = ref([])

const getBUKU = async () => {
    const { data, error } = await supabase.from('BUKU').select('*, kategori(*)')
    .ilike('judul','%${keyword.value}%')
    if(data) BUKU.value = data
}
onMounted(() => {
    getBUKU()
})
</script>

<style scoped>
.card-body {
    width: 100%;
    height: 20em;
    padding: 0;
}
.cover {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: 0 30;
}
</style>