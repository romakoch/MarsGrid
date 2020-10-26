<template>
  <div class="father">
    <h2>Nasa</h2>
    <div class="main" v-bind:style="makeGrid(this.numOfColAndRows[0], this.numOfColAndRows[1])">
     <div class="grid_item" v-for='(img, index) in marsPhotos' v-bind:key="index">
          <Images v-bind:src="img.img_src"/>
          <div class="p_father">
          <div>id: {{img.id}}</div>
          <div>Earth's date: {{img.earth_date}}</div>
          <div>Camera's id: {{img.camera.id}}</div>
          <div>Camera's name: {{img.camera.name}}</div>
          <div>Camera's full name: {{img.camera.full_name}}</div>
          <div>Camera's rover id: {{img.camera.rover_id}}</div>
          <div>Rover's name: {{img.rover.name}}</div>
          <div>Rover's id: {{img.rover.id}}</div>
          <div>Rover's landing date: {{img.rover.landing_date}}</div>
          <div>Rover's launch date: {{img.rover.launch_date}}</div>
          <div>Rover's status: {{img.rover.status}}</div>
          <div>Sol: {{img.sol}}</div>
        </div>
     </div>
    </div>
  </div>
</template>

<script>

import axios from "axios";

import Images from '@/components/Images.vue'

export default {
  name: 'Nasa',
  props: ['numOfColAndRows'],
  data() {
    return {
      marsPhotos: [],
      marsPhotosApiUrl: 'https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&page=1&api_key=wKduKTjycJEpPeN4bBqC1JxUiVo8HpjhQgXahCb1',
      // numofColumns: 4,
      // numsofRows:8,
    };
  },
  components: {
    Images,
  },
  methods: {
    getApiData() {
      axios({
        url: this.marsPhotosApiUrl,
        method: 'GET'
      }).then((response) => {
        const dataPage = response.data;
        console.log(dataPage)
        for (let key in dataPage.photos) {
          this.marsPhotos.push(dataPage.photos[key])
        }
        // console.log(this.marsPhotos[0].img_src)
      });
    },
    makeGrid(c,r) {
      return `grid-template-columns: repeat(${c}, minmax(50px, 1fr));grid-template-rows: repeat(${r}, minmax(300px, 1fr))`
    }
  },
  computed: {

  },
  beforeMount() {
    this.getApiData();
  },
  mounted() {
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
img ~ div {
  visibility: hidden;
}
.grid_item:hover div{
  visibility: visible;
}
.grid_item:hover img{
  height: 2fr;
  width: 2fr;
  filter: brightness(0.3);
  z-index: 0;
}
.father {
  max-height: 100vh;
}
.main {
  display: grid;
  grid-gap: 10px;
  /*grid-template-columns: repeat(4, minmax(100px, 1fr));*/
  /*grid-template-rows: repeat(8, minmax(100px, 1fr));*/
}
.grid_item {
    background-color: #000;
    position: relative;
}
.grid_item img{
    position: absolute;
    left:50%;
    top:50%;
    transform: translate(-50%, -50%);
    max-width:100%;
    max-height: 100%;
    z-index: 10;
}
.p_father {
  position: absolute;
  left: 10%;                      
}
.grid_item div {
  color: #fff;
  margin-left: 10%;
  font-size: 10px;
  z-index: 100;
}
</style>
