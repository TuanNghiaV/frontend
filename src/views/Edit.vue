<template>
   <div>
     <h1>Edit Word</h1>
     <form @submit.prevent="onSubmit">
       <div class="ui labeled input fluid">
         <div class="ui label">
           <i class="united kingdom flag"></i>
           English
         </div>
         <input type="text" required v-model="word.english"/>
       </div>
       <br />
       <div class="ui labeled input fluid">
         <div class="ui label">
           <i class="germany flag"></i>
           German
         </div>
         <input type="text" required v-model="word.german"/>
       </div>
       <br />
       <button class="ui primary button">Submit</button>
     </form>
   </div>
 </template>
 
 <script>
 import { ViewWord, UpdateWord } from "../helpers/api";
 
 export default {
   name: "Edit",
   data() {
     return {
       word: {
       }
     };
   },
   async mounted() {
     try {
       this.word = await ViewWord(this.$route.params.id);
     } catch (error) {
       console.error("Error fetching word:", error);
       alert("Failed to fetch word details. Please try again.");
     }
   },
   methods: {
     async onSubmit() {
       try {
         // Save updated word to database
         await UpdateWord(this.$route.params.id, this.word);
         // Redirect to word list page
         this.$router.push("/words");
       } catch (error) {
         console.error("Error updating word:", error);
         alert("Failed to update word. Please try again.");
       }
     }
   }
 };
 </script>
 