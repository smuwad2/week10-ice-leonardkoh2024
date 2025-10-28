<script>

    export default {
        // Add code if/as necessary
        // Hint: Add properties subject, entry and mood
        data(){
            return {
                moods:{
                    "angry":"/assets/angry.png",
                    "happy":"/assets/happy.png",
                    "sad":"/assets/sad.png"
                }
            }
        },
        props:{
            subject: String,
            entry: String,
            mood: String
        }
    }
</script>


<template>
    <!-- TODO: add your template code here. Use boostrap card --> 
    <div class="card" style="width: 18rem;">
    <img class="card-img-top" :src="moods[mood.toLowerCase()]" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">{{ subject }}</h5>
    <p class="card-text">{{ entry }}</p>
  </div>
</div>
</template>

