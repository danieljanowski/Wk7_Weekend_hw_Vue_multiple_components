<template>
  <div>
    <h1>SpaceX</h1>
    <mission-list :spaceXData="spaceXData"></mission-list>
    <!-- <div v-for="(launch, index) in spaceXData">
          <img :src=launch.links.mission_patch_small alt="mission-logo" height="75">
          <p>{{index}}: {{launch.mission_name}} - {{Date(launch.launch_date_unix)}} - Success: launch: {{launch.launch_success}} - recovery: {{launch.rocket.fairings}} <a :href=launch.links.video_link>Video</a></p>
          <p>{{launch.details}}</p>
          <img :src=launch.links.flickr_images[0] alt="image" height="250">
          <hr> -->
    </div>
  </div>
</template>

<script>
import MissionList from "@/components/MissionList.vue";

export default {
    name: "app",
    components: {
      "mission-list": MissionList,
    },

    data(){
    return {
      spaceXData: [],
    }
  },

  mounted(){
    fetch('https://api.spacexdata.com/v3/launches/')
    .then(apiData => apiData.json())
    .then(apiDataJson => this.spaceXData = apiDataJson)
  }
}
</script>

<style scoped>
  body{
    background-color: grey;
  }
  h1{text-align: center;}
</style>