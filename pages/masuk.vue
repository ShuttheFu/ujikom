<template>
  <div>
    <table>
      <tr>
        <th>No</th>
        <th>tanggal masuk</th>
        <th>Nama barang</th>
        <th>Deskripsi</th>
        <th>jumlah</th>
      </tr>
      <tr v-for="(data, index) in datas" :key="data.id">
        <th>{{ index + 1 }}</th>
        <th>{{ data.created_at }}</th>
        <th>{{ data.id_barang.nama_barang }}</th>
        <th>{{ data.asal_barang }}</th>
        <th>{{ data.jumlah }}</th>
      </tr>
    </table>
  </div>
</template>

<script setup>
const supabase = useSupabaseAuthClient();
const datas = ref([]);
const getData = async () => {
  const { data, error } = await supabase.from("barang_in").select("id,created_at,id_barang(id,nama_barang),asal_barang").order("created_at", { ascending: false });
  datas.value = data;
};
onMounted(() => {
  getData();
});
</script>
