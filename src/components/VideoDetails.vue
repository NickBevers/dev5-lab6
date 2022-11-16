<script setup>
    import { ref, onMounted } from 'vue';

    const videoDataUrl = "/tiktok.json";
    let username = ref('');
    let description = ref('');

    onMounted(() => {
        console.log('mounted');
        fetch(videoDataUrl)
            .then(res => res.json())
            .then(data => { 
                username.value = data.videos[0].username;
                description.value = data.videos[0].description;
            })
    });
</script>

<template>
    <div class="video__details">
        <h3>{{username}}</h3>
        <p>{{description}}</p>
    </div>
</template>

<style scoped>
    .video__details {
        padding: 0 1rem;
    }
</style>
