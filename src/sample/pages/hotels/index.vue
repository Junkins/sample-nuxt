<template>
  <section class="container">
    <el-col :span="6" v-for="hotel in hotels" :key="hotel.id" class="col-style">
      <el-card :body-style="{ padding: '15px' }" class="box-card">
        <div class="bottom content-style text">
          <div slot="header">
            <div>{{ hotel.name }}</div>
          </div>
          <div class="bottom content-style text">
            <div>{{ hotel.address }}</div>
            <el-rate v-model="hotel.rating" :colors="['#2F3D4D', '#64B486', '#4B7C6E']"></el-rate>
          </div>
          <div>
            <GmapMap
                :center="{lat:hotel.lat, lng:hotel.lng}"
                :zoom="15"
                map-type-id="terrain"
                style="width: 500px; height: 300px"
            >
                <GmapMarker
                    :key="index"
                    :position="{lat:hotel.lat, lng:hotel.lng}"
                    :clickable="true"
                    :draggable="true"
                />
            </GmapMap>
          </div>
        </div>
      </el-card>
    </el-col>
  </section>
</template>

<script>
export default {
  data(){
    return {
      hotels: [],
      markers: [
        {position: { lng: 10.2, lat: 10 }},
        {position: { lng: 10.1, lat: 10 }}
      ]
    }
  },
  async asyncData({ app }) {
    const response = await app.$axios.$get('http://192.168.56.110/hentai/google_map.php');
    return { hotels: response.hotels };
  }
}
</script>

<style>
  .content-style {
    line-height: 30px;
    font-size: 14px;
  }

  .tab-style {
    margin-right: 5px;
  }

  .box-card {
    height: 360px;
    font-size: 15px;
  }

  .col-style {
    padding: 10px;
  }

  .page-component-up {
    background-color: #59bb0c;
    position: fixed;
    right: 80px;
    bottom: 80px;
    width: 40px;
    height: 40px;
    border-radius: 20px;
    cursor: pointer;
    transition: 0.3s;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.12);
  }

  .page-component-up i {
    color: #fff;
    display: block;
    line-height: 40px;
    text-align: center;
    font-size: 18px;
  }

  a:link,
  a:visited {
    color: #59bb0c;
  }

  a:hover {
    color: #3b8070;
  }
</style>