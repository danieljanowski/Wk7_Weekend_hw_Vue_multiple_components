<template>
    <div v-if="mission">
        <hr>
        <img v-if="mission.links.mission_patch_small" :src=mission.links.mission_patch_small alt="mission-logo" height="200" class="logo">
        <h2>{{mission.mission_name}}</h2> <hr>
        <p class="center_text">{{mission.details}}</p><hr>
        <p>Launch date: {{Date(mission.launch_date_unix)}} </p>
        <p v-if="mission.rocket.rocket_name">Rocket name: {{mission.rocket.rocket_name}}, rocket type: {{mission.rocket.rocket_type}}</p>
        <p v-if="mission.launch_site.site_name_long">Launch site: {{mission.launch_site.site_name_long}}</p>
        <div v-if="mission.rocket.second_stage.payloads[0].payload_id">
            <p> Payload: {{mission.rocket.second_stage.payloads[0].payload_id}} 
            {{mission.rocket.second_stage.payloads[0].payload_id}} {{mission.rocket.second_stage.payloads[0].payload_type}} </p>
            <p> {{mission.rocket.second_stage.payloads[0].customers[0]}} 
            <!-- {{mission.rocket.second_stage.payloads[0].payload_manufacturer}}  -->
            {{mission.rocket.second_stage.payloads[0].nationality}} </p>
        </div>
            <!-- Success: launch: {{mission.launch_success}} - recovery: {{mission.rocket.fairings}}  -->
        <p v-if="mission.links.video_link">Video from the launch: <a class="center_img" :href=mission.links.video_link >Video</a></p> <br>
        <span v-for="image in mission.links.flickr_images">
            <img class="center_img" :src=image alt="image" height="250">
        </span>
    </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: "mission-detail",

    data(){
        return {
            mission: null,
        }
    },

    mounted(){
        eventBus.$on('selected-mission', (mission) => {
            this.mission = mission
        })
    },

    methods: {

    }

}
</script>

<style scoped>
    .logo {
        display: block;
        margin-left: auto;
        margin-right: auto;
        align-items: center;
        padding: 20px;
    }
    .center_img {
        /* display: block; */
        margin-left: auto;
        margin-right: auto;
        align-items: stretch;
        padding: 20px;
    }

    h2 {text-align: center;}

    .center_text {
        text-align: center;
        font-size: 0.7em;
    }
    p {font-size: 1em;}
</style>