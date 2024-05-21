<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">riwayat kunjungan</h2>
                <div class="my-3">
                    <form  @submit.prevent="getBuku">
                        <input v-model="keyword" type="search" class="form-control rounded-5" placeholder="Fiter...">
                    </form>
                </div>
                <div class="my-3 text-muted">menampilkan daftar </div>
                 <table class="table">
                    <thead>
                        <tr>
                            <td>#</td>
                            <td>NAMA</td>
                            <td>KEANGGOTAAN</td>
                            <td>WAKTU</td>
                            <td>KEPERLUAN</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(visitor,i) in visitors" :key="i">
                            <td>{{ i+1 }}.</td>
                            <td>{{ visitor.nama }}</td>
                            <td>{{ visitor.keanggotaan.nama }}</td>
                            <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
                            <td>{{ visitor.keperluan.nama }}</td>
                        </tr>
                    </tbody>
                 </table>
            </div>
        </div>
        <NuxtLink to="/pengunjung/tambah">
            <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">kembali</button>
        </NuxtLink>
    </div>
</template>
<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])

const getPengunjung = async () => {
    const { data, error } = await supabase.from('Pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
    if(data) visitors.value = data
}
const getBuku = async () => {
    const { data, error} = await supabase
    .from('Pengunjung')
    .select(`*,nama(*)`)
    .ilike("judul", `%${keyword.value}%`);
    if(data) books.value= data;
};

onMounted(() => {
    getPengunjung()
    getBuku()
})
</script>