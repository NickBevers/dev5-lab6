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
        <ul class="commentList">
            <li v-for="comment in comments.comments" :key="comment.id">
                <div class="comment">
                    <h3>{{comment.user}}</h3>
                    <p>{{comment.text}}</p>
                </div>
            </li>
        </ul>

        <div class="messageForm">
            <input type="text" placeholder="Enter your message" v-model="message" />
            <button @click="addMessage">Add Message</button>
        </div>
    </div>
</template>

<style scoped>
    .comments {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .commentList {
        list-style: none;
        display: flex;
        flex-direction: column-reverse;
        padding: 0 1rem;
        height: 75vh;
        overflow-y: auto;
        scrollbar-width: thin;
        scrollbar-color: rgb(149, 197, 238) #ffffff;
    }

    ::-webkit-scrollbar-thumb {
        border-radius: 10px;
    }

    h3 {
        margin: 0;
    }

    p {
        margin-top: 0;
    }

    .messageForm{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .messageForm input {
        width: 76%;
        padding: 10px;
        margin-bottom: 10px;
    }

    .messageForm button {
        width: 80%;
        padding: 10px;
        background-color: rgb(149, 197, 238);
        color: #ffffff;
        border: none;
        border-radius: 5px;
    }
</style>
