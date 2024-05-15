<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">ISI BUKU KUNJUNGAN</h2>
        <form @submit.prevent="kirimData" >
          <div class="mb-3">
            <input v-model="form.nama" type="text" placeholder="nama...">
          </div>
          <div class="mb-3">
            <select v-model="form.keanggotaan"> 
              <option value="">KEANGGOTAAN</option>
                <option v-for="(member,i) in members" :key="i" :value="member.id">{{ member.nama }}</option> 
            </select>
          </div>
          <div class="mb-3">
            <div class="row">
              <div class="col-md-4">
                <select v-model="form.tingkat">
                  <option value="">TINGKAT</option>
                  <option value="X">X</option> 
                  <option value="XI">XI</option>
                  <option value="XII">XII</option>           
                </select>
              </div>
              <div class="col-md-4">
                <select v-model="form.jurusan">
                  <option value="">JURUSAN</option>
                  <option value="PPLG">PPLG</option>
                  <option value="TKJT">TKJT</option>
                  <option value="TSM">TSM</option>
                  <option value="DKV">DKV</option>
                  <option value="TOI">TOI</option>
                </select>
              </div>
              <div class="col-md-4">
                <select v-model="form.kelas">
                  <option value="">KELAS</option>
                  <option value="1">1</option>
                  <option value="2">2</option>
                  <option value="3">3</option>
                  <option value="4">4</option>
                </select>
              </div>
            </div>
          </div>
          <div class="mb-3">
            <select v-model="form.keperluan">
              <option value="">KEPERLUAN</option>
              <option v-for="(item, i) in objectives" :key="i" :value="item.id">{{ item.nama }}</option>
            </select>
          </div>
          <nuxt-link to="/pengunjung">
            <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">KIRIM</button>
          </nuxt-link>
        </form>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const members = ref([])
const objectives = ref([])

const form = ref({
  Nama: "",
  Keanggotaan: "",
  Tingkat: "",
  Jurusan: "",
  Kelas: "",
  Keperluan: "",
})

const kirimData = async () => {
  const {error} = await supabase.form('pengunjung').insert([form.value])
  if(!error) navigateTo('/pengunjung')
}

const getKeanggotaan = async () => {
  const { data, error } = await supabase.form('keanggotaan').select('*')
  if(data) members.value = data
}

const getKeperluan = async () => {
  const { data, error } = await supabase.form('keperluan').select('*')
  if(data) members.value = data
}

onMounted(() => {
  getKeanggotaan()
  getKeperluan()
})
</script>

<form @submit.prevent="KirimData"></form>

