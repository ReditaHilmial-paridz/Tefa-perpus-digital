<template>
    <h2 class="text-start my-4">{{ buku.judul }}</h2>
    <div class="row">
        <div class="col-md-5">
            <span v-if="buku.cover"><img src="buku.cover" class="cover" alt="cover"></span>
            <span v-else><img src="https://www.google.com/url?sa=i&url=https%3A%2F%2Fralfvanveen.com%2Fen%2Fglossary%2Fplaceholder%2F&psig=AOvVaw03kQl7CsBMnBiP9AUqM2nY&ust=1714456536412000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCPi05Lve5oUDFQAAAAAdAAAAABAD" :alt="buku.judul"></span>
        </div>
        <div class="col-md-6">
            <ul class="list-group list-group-flush">
                <li class="list-group-item">penulis : {{ buku.penulis }}</li>
                <li class="list-group-item">tahun_terbit : {{ buku.tahun_terbit }}</li>
                <li class="list-group-item">penerbit : {{ buku.penerbit }}</li>
                <li class="list-group-item">rak : {{ buku.rak }}</li>
                <li class="list-group-item">deskripsi : {{ buku.deskripsi }}</li>
            </ul>
        </div>
    </div>
</template>
<script setup>
import { useRoute } from 'vue-router';

const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref([])


const getBookById = async () => {
    const { data, error } = await supabase.from('buku').select('*, kategori(*)')
    .eq('id', route.parans.id)
    if(data) buku,value = data[0]
}


onMouted(() => {
    getBookById()
})
</script>

