<template>
  <div>
    <NuxtLink to="/keluar">Lihat Barang Keluar</NuxtLink>
    <form @submit.prevent="addOutBarang">
      <div>
        <label for="" style="display: block">Pilih nama barang</label>
        <select name="" id="" v-model="barang">
          Pilih Barang
          <option v-for="data in datas" :key="data.id" :value="data.id">{{ data.nama_barang }}</option>
        </select>
      </div>
      <div>
        <label for="">jumlah barang</label>
        <input type="text" v-model="jumlah" />
      </div>
      <div>
        <label for="">destinasi barang</label>
        <input type="text" v-model="destinasi" />
      </div>
      <button type="submit">tambah</button>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const barang = ref();
const destinasi = ref();
const datas = ref([]);
const jumlah = ref();
const addOutBarang = async () => {
  const { data, error } = await supabase.from("barang_out").insert({
    id_barang: barang.value,
    destinasi: destinasi.value,
    jumlah: jumlah.value,
  });
  alert("berhasil");
  if (error) {
    console.log(error);
  }
};
const getData = async () => {
  const { data, error } = await supabase.from("barang").select();
  datas.value = data;
};
onMounted(() => {
  getData();
});
</script>
