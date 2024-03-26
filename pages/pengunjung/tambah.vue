<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">isi buku kunjungan</h2>
                <form @submit.prevent="kirimdata">
                    <div class="mb-3">
                        <input v-model="form.nama" class="form-control form-control-lg rounded-5" type="text" placeholder="nama..."/>
                    </div>
                    <div class="mb-3">
                        <select v-model="form.keanggotaan"  class="form-control form-control-lg form-select rounded-5">
                            <option value="">keanggotaan</option>
                            <option v-for="(member, i) in members" :key="i" :value="member.id">{{ member.nama }}</option>
                        </select>
                    </div>
                    <div class="mb-3">
                        <div class="row">
                            <div class="col-md-4">
                                <select v-model="form.tingkat" class="form-control form-control-lg form-select rounded-5 mb-2">
                                    <option value="">tingkat</option>
                                    <option value="X">X</option>
                                    <option value="XI">XI</option>
                                    <option value="XII">XII</option>
                                </select>
                            </div>
                            <div class="col-md-4">
                                <select v-model="form.jurusan" class="form-control form-control-lg form-select rounded-5 mb-2">
                                    <option value="">jurusan</option>
                                    <option value="PPLG">PPLG</option>
                                    <option value="TJKT">TJKT</option>
                                    <option value="TSM">TSM</option>
                                    <option value="DKV">DKV</option>
                                    <option value="TOI">TOI</option>
                                </select>
                            </div>
                            <div class="col-md-4">
                                <select v-model="form.kelas" class="form-control form-control-lg form-select rounded-5 mb-2">
                                    <option value="">kelas</option>
                                    <option value="1">1</option>
                                    <option value="2">2</option>
                                    <option value="3">3</option>
                                    <option value="4">4</option>
                                </select>
                            </div>
                        </div>
                    </div>
                    <div class="mb-3">
                        <select v-model="form.keperluan" class="form-control form-control-lg form-select rounded-5 mb-2">
                            <option value="">keperluan</option>
                            <option v-for="(item, i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
                        </select>
                    </div>
                        <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">kirim</button>
                </form>
            </div>
        </div>
    </div>
</template>
<script setup>
const supabase = useSupabaseClient()

const members = ref([]);
const objectives = ref([]);

const form = ref({
    nama: "",
    keanggotaan:"",
    tingkat:"",
    jurusan:"",
    kelas:"",
    keperluan:"",
});

const kirimdata = async () => {
    const { error } = await supabase.form('Pengunjung').insert([form.value])
    if(!error) navigateTo('/pengunjung')
};

const getkeanggotaan = async () => {
    const { data, error } = await supabase.form('keanggotaan').select('*')
    if(data) members.value = data
};

const getkeperluan = async () => {
    const { data, error } = await supabase.form('keperluan').select('*')
    if(data) objectives.value = data
};

onMounted(() => {
    getkeanggotaan();
    getkeperluan();
});
</script>