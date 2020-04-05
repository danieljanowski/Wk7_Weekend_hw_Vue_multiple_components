<template>
    <div>
        <form v-on:submit.prevent>
    <!-- <input type="text" v-model="search" placeholder="search for country..." v-on:keyup="searchForCountry"> -->
            <select v-on:change="handleSelect" v-model="selectedMissionFromList">
                <option disabled value="">Select a mission...</option>
                <option v-for="mission in spaceXData" :value="mission">{{mission.mission_name}}</option>
            </select>
        </form>
    </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: "mission-list",
    props: ["spaceXData"],
    data(){
        return{
            "selectedMissionFromList": {},
        }
    },
    methods: {
        handleSelect(){
            eventBus.$emit('selected-mission', this.selectedMissionFromList)
        }

    },
};

</script>

<style scoped>

</style>