<template>
    <div class="container-fluid">
      <div class="row"> 
        <div class="col-lg-12">
          <div class="my-3">
            <form @submit.prevent="getBuku">
            <input
              v-model="keyword"
              type="search"
              class="form-control rounded-5"
              placeholder="mau baca apa hari ini?"
              />
            </form>
          </div>
          <div class="my-3 text-muted">menampilkan {{ books?.length }} dari {{ totalBuku }}</div>
          <div class="row justify-content-evenly">
            <div v-for="(buku, i) in books" :key="i" class="col-lg-2">
            <nuxt-link :to="`/buku/${buku.id}`">
                <div class="card mb-3">
                  <div class="card-body">
                    <img :src="buku.cover" class="cover" :alt="buku.judul" />
                  </div>
                </div>
              </nuxt-link>
              </div>
            </div>
          </div>
        </div>
      </div>
      <nuxt-link to="/">
        <button type="submit" class="btn btn-light btn-lg rounded-5 px-5">kembali</button>
      </nuxt-link>
  </template>
  
  <script setup>
  const supabase = useSupabaseClient();
  const totalBuku = ref(0);
  const books = ref([])

  const getBuku = async () => {
    const { data, error} = await supabase
    .from('Buku')
    .select(`*,kategori(*)`)
    .ilike("judul", `%${keyword.value}%`);
    if(data) books.value= data;
  
  };
  const getTotalBuku = async () => {
  const { count, error } = await supabase.from("Buku").select("*, kategori(*)", { count: 'exact', head: true });
  if (count) totalBuku.value = count;
};

  onMounted(() => {
    getBuku();
    getTotalBuku();
  });

  const keyword = ref("");
  </script>

  <style scoped>
  .card-body {
    width: 100%;
    height: 30em;
    padding: 0;
  }
  .cover {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: 0 30;
  }
  .form-control {
    background-color: #D9D9D9;
  }
  .btn {
    background-color: #D9D9D9;
  }
  </style>