<template>
  <div>
    <section class="flex-container">
      <header class="flex-item header"><img src="https://www.spacex.com/sites/spacex/files/spacex_logo_white.png" alt="logo"></header>
      <aside class="flex-item sidebar">
      </aside>
      <main class="flex-item main">
        <h1>SpaceX Mission Database</h1>
        <mission-list :spaceXData="spaceXData"></mission-list>
        <div v-if="selectedMission"><mission-detail></mission-detail></div>
      </main>
      <aside class="flex-item sidebar">
      </aside>
    </section>
  </div>
</template>

<script>
import MissionList from "@/components/MissionList.vue";
import MissionDetail from "@/components/MissionDetail.vue";

export default {
    name: "app",
    components: {
      "mission-list": MissionList,
      "mission-detail": MissionDetail,
    },

    data(){
    return {
      spaceXData: [],
      selectedMission: {},
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

.flex-container {
  padding: 0;
  margin: 0;
  list-style: none;
  height: 200px;
  display: flex;
  justify-content: space-around;
  flex-flow: row wrap;
  align-items: stretch;
}
.header {
  height: 50px;
  flex: 1 100%;
  text-align: center;
  background-color: black;
}
.sidebar {
  flex: 1;
}
.main {
  flex: 20;
}
.flex-item {
  /* background: tomato; */
  padding: 10px;
  width: 100px;
  border: 1px none black;
  color: black;
  font-weight: normal;
  font-size: 1.5em;
  text-align: left;
  font-family: 'Hind', sans-serif;
}
.sidebar {
  flex: 1;
}
h1 {text-align: center;}

</style>