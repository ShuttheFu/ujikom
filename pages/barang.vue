<template>
  <div>
    <NuxtLink to="/tambah">tambah Barang</NuxtLink>
    <table>
      <tr>
        <th>No</th>
        <th>Nama barang</th>
        <th>Deskripsi</th>
      </tr>
      <tr v-for="(data, index) in datas" :key="data.id">
        <th>{{ index + 1 }}</th>
        <th>{{ data.nama_barang }}</th>
        <th>{{ data.deskripsi }}</th>
      </tr>
    </table>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const datas = ref([]);
const getData = async () => {
  const { data, error } = await supabase.from("barang").select();
  datas.value = data;
};
onMounted(() => {
  getData();
});
</script>
