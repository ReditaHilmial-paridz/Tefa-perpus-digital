<template>
    <div>
        <h2 class="text-start my-4">{{ buku.judul }}</h2>
        <div class="row">
            <div class="col-md-3">
                <div class="card">
                    <div class="card-body">
                        <span v-if="buku.cover"><img :src="buku.cover" :alt="buku.judul"></span>
                <span v-else><img src="https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.svgrepo.com%2Fsvg%2F508699%2Flandscape-placeholder&psig=AOvVaw2-SWmfk33NzXubPfqn0P16&ust=1714794757874000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCNjln7nK8IUDFQAAAAAdAAAAABAE://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.svgrepo.com%2Fsvg%2F508699%2Flandscape-placeholder&psig=AOvVaw2-SWmfk33NzXubPfqn0P16&ust=1714794757874000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCNjln7nK8IUDFQAAAAAdAAAAABAE"></span>
                    </div>
                </div>
            </div>
            <div class="col-md-6">
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">penulis : {{  buku.penulis }}</li>
                    <li class="list-group-item">tahun_terbit : {{  buku.tahun_terbit }}</li>
                    <li class="list-group-item">rak : {{ buku.rak }}</li>
                    <li class=" list-group-item">deskripsi : {{ buku.deskripsi }}</li>
                </ul>
            </div>
        </div>
        <NuxtLink to="/buku">
            <button type="submit" class="btn btn-lg rounded-5 px-5">kembali</button>
        </NuxtLink>
    </div>
</template>

<script setup>
import { onMounted } from 'vue';

const supabase = useSupabaseClient()
const route = useRoute()
const buku = ref([])

const getBukuByID = async () => {
    const { data, error } = await supabase.from('buku').select(', kategori()')
    .eq('id', route.params.id)
    if(data) buku.value = data[0]
}

onMounted(() => {
    getBukuByID()
})
</script>