<script setup>
const supabase = useSupbaseClient()

const books = ref([])

const keyword = ref('')

const getBooks = async () => {
  const { data, error } = await supabase.form('buku').select(`*, kategori(*)`)
  .ilike('judul', `%${keyword.value}%`)
  if(data) books.value = data
}


onMounted(() => {
  getBooks()
})


</script>

<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">BUKU</h2>
        <div class="my-3">
          <form @submit.prevent="getBooks">
            <input v-model="keyword" type="serch">
          </form>
        </div>
      </div>
      <div class="my-3 text-muted">menampilkan {{ books.length }} dari {{ jumlah }}</div>
      <div class="row">
        <div v-for="(book, i) in books" :key="i" class="col-lg-2">
          <div class="card-mb-3">
            <div class="card-body">
              <nuxt-link :to="`Buku/${book.id}`">
                <img :src="`book.cover`" class="cover" alt="cover">
              </nuxt-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>    
</template>
<button type="submit" class="btn btn-lg rounded-5 px-5 pl-5">Menu</button>  

<style scoped>
.container-fluid {
  background-image: url(assets/img/yy.webp);
  height: 100;
  background-position: center;
  background-repeat: repeat;
  background-size: cover;
}
.card-body {
  width: 100%;
  height: em;
  padding: 0;
}
.cover {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}

.btn {
  background-color: rgb(14, 154, 235);
}
</style>
