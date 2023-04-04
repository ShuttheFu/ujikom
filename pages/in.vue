<template>
  <div>
    <NuxtLink to="/masuk">Lihat Barang masuk</NuxtLink>
    <form @submit.prevent="addInbarang">
      <div>
        <label for="" style="display: block">Pilih nama barang</label>
        <select name="" id="" v-model="barang">
          Pilih Barang
          <option v-for="data in datas" :key="data.id" :value="data.id">{{ data.nama_barang }}</option>
        </select>
      </div>
      <div>
        <label for="">asal barang</label>
        <input type="text" v-model="asal" />
      </div>
      <button type="submit">tambah</button>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const barang = ref();
const asal = ref();
const datas = ref([]);
const addInbarang = async () => {
  const { data, error } = await supabase.from("barang_in").insert({
    id_barang: barang.value,
    asal_barang: asal.value,
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
