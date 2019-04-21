<template>
  <section class="container">
    <el-col :span="6" v-for="hotel in hotels" :key="hotel.id" class="col-style">
      <el-card :body-style="{ padding: '15px' }" class="box-card">
        <div class="bottom content-style text">
          <div>{{ hotel.name }}</div>
          <div>{{ hotel.address }}</div>
          <el-rate v-model="hotel.rating" :colors="['#2F3D4D', '#64B486', '#4B7C6E']"></el-rate>
        </div>
      </el-card>
    </el-col>
  </section>
</template>

<script>
export default {
  data(){
    return {
      hotels: []
    }
  },
  async asyncData({ app }) {
    const response = await app.$axios.$get('http://192.168.56.110/hentai/google_map.php');
    return { hotels: response.hotels };
  }
}
</script>