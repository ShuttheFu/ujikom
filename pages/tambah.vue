<template>
  <div>
    <NuxtLink to="/barang">Lihat Barang</NuxtLink>
    <form @submit.prevent="addBarang">
      <div>
        <label for="" style="display: block">Pilih nama barang</label>
        <input type="text" v-model="nama" />
      </div>
      <label for="">deskripsi barang</label>
      <div>
        <textarea name="" id="" cols="30" rows="10" v-model="deskripsi"></textarea>
      </div>
      <button type="submit">tambah</button>
    </form>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const nama = ref();
const deskripsi = ref();
const datas = ref([]);
const addBarang = async () => {
  const { data, error } = await supabase.from("barang").insert({
    nama_barang: nama.value,
    deskripsi: deskripsi.value,
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
