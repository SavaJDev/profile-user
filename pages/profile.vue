<template>
   <v-container class="container">
     <v-row align="center" v-if="!show" class="loading">
         <v-progress-linear :indeterminate="true"></v-progress-linear>
     </v-row>
     <v-row v-else="show">
         <v-col cols="4" class="colFoto">
             <v-row justify="center">
                <img src="../static/foto.png" alt="foto">  
             </v-row>
         </v-col>
         <v-col>
              <h1>Name: {{userName}}</h1>
              <h1>E-mail: email@mail.ru</h1> 
         </v-col>
     </v-row>
   </v-container>
</template>


<script>
    import {mapState} from 'vuex'
    export default {
        data: () => ({
           show: false  
        }),
        middleware: ["profile"],
        computed: {
          ...mapState(["user"]),
          userName(){
            let str = this.user.name
            
             return str.charAt(0).toUpperCase() + str.slice(1)
          }    
        },
        created(){
           setTimeout(() => this.show = true, 2000)
        }
    }
</script>

<style scoped>
    .container {
       height: 80vh;    
    }
    
    .loading {
        height: 100%;
    }
    
    .colFoto {
        box-shadow: 0 0 10px rgba(0,0,0,0.5); 
        margin-right: 10px;
    }
    
    .colFoto img {
        width: 17rem;
    }
</style>