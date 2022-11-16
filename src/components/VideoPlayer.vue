<script setup>
    import { ref, reactive, onMounted, onUnmounted } from 'vue';
    import "animate.css";
    
    const videoDataUrl = "/tiktok.json";
    let src = ref('');
    let videoList = reactive({ videos : []});
    let animation = ref('');
    
    onMounted(() => {
        fetch(videoDataUrl)
        .then(res => res.json())
        .then(data => {
            console.log(data);
            console.log(data.videos[0].video);
            // set src to the first video in the array
            src.value = data.videos[0].video;
            videoList.videos = data.videos;
        })
    })

    const nextVideo = () => {
        animation.value = 'animate__fadeOut';
        setTimeout(() => {
            animation.value = 'animate__fadeIn';
            src.value = videoList.videos[1].video;
        }, 1000);
    }
</script>

<template>
    <div class="video">
        <div class="controls">
            <a  href="#" class="controls__next" @click="nextVideo()"> ↓</a>
        </div>
        <video :class="animation" class="animate__animated" :src="src" controls autoplay muted></video> 
    </div>
</template> 

<style scoped>

    .video {
        position: relative;
        width: fit-content;
    }
    .controls__next {
        position: absolute;
        top: 0;
        right: 0;
        height: 100%;
        z-index: 1;
        display: flex;
        flex-direction: column;
        justify-content: center;
        font-size: 2rem;
        color: black;
        background-color: white;
        text-decoration: none;
    }
</style>
