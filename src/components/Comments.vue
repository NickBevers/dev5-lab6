<script setup>
    import { ref, reactive, onMounted } from 'vue';
    let comments = reactive({ comments: [] });
    let message = ref('');

    onMounted(() => {
        fetch('https://lab5-p379.onrender.com/api/v1/messages')
            .then(res => res.json())
            .then(data => {
                console.log(data);
                comments.comments = data;
            })
    })

    const addMessage = () => {
        console.log(message.value);
        let data = {
            user: 'Anonymous',
            text: message.value  
        }
        fetch('https://lab5-p379.onrender.com/api/v1/messages', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        })
            .then(res => res.json())
            .then(data => {
                console.log(data);
                comments.comments.push({
                    _id: data.data._id,
                    user: data.data.user,
                    text: data.data.text
                });
            })
    }
</script>

<template>
    <div class="comments" >
        <ul>
            <li v-for="comment in comments.comments" :key="comment.id">
                <div class="comment">
                    <h3>{{comment.user}}</h3>
                    <p>{{comment.text}}</p>
                </div>
            </li>
        </ul>

        <input type="text" placeholder="Enter your message" v-model="message" />
        <button @click="addMessage">Add Message</button>
    </div>
</template>

<style scoped>

</style>
