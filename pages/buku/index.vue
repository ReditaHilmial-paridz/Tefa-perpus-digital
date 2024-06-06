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
        <div class="my-3 text-muted">
          menampilkan {{ books?.length }} dari {{ totalBuku }}
        </div>
        <div class="row justify-content-evenly">
          <div
            v-for="(buku, i) in books"
            :key="i"
            class="col-6 col-lg-2 d-flex"
          >
            <div class="card flex-fill mb-3 shadow-lg">
              <div class="card-body">
                <nuxt-link :to="`/buku/${buku.id}`">
                  <img :src="buku.cover" class="cover" :alt="buku.judul" />
                </nuxt-link>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <nuxt-link to="/">
      <button type="submit" class="btn btn-light btn-lg rounded-5 px-5">
        kembali
      </button>
    </nuxt-link>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();
const totalBuku = ref(0);
const books = ref([]);

const getBuku = async () => {
  const { data, error } = await supabase
    .from("Buku")
    .select(`*,kategori(*)`)
    .ilike("judul", `%${keyword.value}%`);
  if (data) books.value = data;
};
const getTotalBuku = async () => {
  const { count, error } = await supabase
    .from("Buku")
    .select("*, kategori(*)", { count: "exact", head: true });
  if (count) totalBuku.value = count;
};

onMounted(() => {
  getBuku();
  getTotalBuku();
});

const keyword = ref("");
</script>

<style scoped>
.shadow-lg {
  box-shadow: 6px 4px 0 #2e2e2eae !important;
}
.card:hover {
  transform: scale(1.05);
  box-shadow: 4px 4px 20px #2e2e2eae !important;
}
.card {
  transition: all 0.2s ease-in-out;
}
.card-body {
  padding: 0;
}
.cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}
.form-control {
  background-color: #d9d9d9;
}
.btn {
  background-color: #d9d9d9;
}
</style>
