<script setup>
import VideoPlayer from './components/VideoPlayer.vue'
import VideoDetails from './components/VideoDetails.vue'
</script>

<template>
    <div class="videoContainer">
        <VideoPlayer title="Video is player" />
        <VideoDetails />

    </div>
</template>

<style scoped>
.videoContainer {
    display: grid;
    grid-template-columns: 9fr 3fr;
}
</style>
