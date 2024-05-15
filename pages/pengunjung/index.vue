<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <input type="serch" class="form-conrol form-control-lg rounded-5" placeholder="Filter..." />
        </div>
        <div class="my-3 text-muted">menampilkan 1 dari 1</div>
        <table class="table">
          <thead>
            <tr>
              <td>No</td>
              <td>Tanggal/Waktu</td>
              <td>Keanggotaan</td>
              <td>Tingkat</td>
              <td>Jurusan</td>
              <td>Kelas</td>
              <td>Keperluan</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in visitor" :key="i">
              <td>{{ i+ 1 }}.</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan.nama }}</td>
              <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
              <td>{{ visitor.tingkat }}</td>
              <td>{{ visitor.keperluan.nama }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])

const getPengunjung = async () => {
  const { data, error } = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
  if(data) visitors.value = data
}

onMounted(() => {
  getPengunjung()
})
</script>


