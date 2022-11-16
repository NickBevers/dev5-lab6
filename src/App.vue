<script setup>
import VideoPlayer from './components/VideoPlayer.vue'
import VideoDetails from './components/VideoDetails.vue'
import Comments from './components/Comments.vue'
</script>

<template>
    <div class="videoContainer">
        <VideoPlayer title="Video is player" />
        <div class="detailCommentsContainer">
            <VideoDetails />
            <Comments />
        </div>
    </div>
</template>

<style scoped>
.videoContainer {
    display: grid;
    grid-template-columns: 9fr 3fr;
}

.detailCommentsContainer{
    display: flex;
    flex-direction: column;
    
}
</style>
