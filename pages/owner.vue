<template>
   <div class="cat-container">
        <h1>Add a new owner</h1>
        <div class="cart-wrapper">
            <div class="wraps">
                  <label for="">name</label>
                  <input type="text" class="cart-input" v-model="name">
            </div>
            <div class="wraps">
                  <label for="">about</label>
                  <input type="text" class="cart-input" v-model="about">
            </div>
            <div class="wraps">
                  <label for="">photo</label>
                  <label for="choosefile button">
                           <input type="file" @change="onFileSelected">
                           <p style="margin-top">{{ fileName }}</p>
                 </label>
            </div>

              <span class="cart-wrapper-button" style="margin-top:10px">
                  <span @click="addOwners">Add owner</span>
            </span>
        </div>

        <ul  v-for="owner in owners"  :key="owner._id">
            <li>{{ owner.name }}</li>
        </ul>
   </div>
</template>

<script>
    export default {
        async asyncData({ $axios }){
            try{
                let response = await $axios.$get("http://localhost:5000/api/owners"); 
                return {
                    owners: response.owners
                }
            }catch(err){
                console.log(err);
            }
        },

        data(){
            return{
               name:"",
               about:"", 
               fileName:"", 
               selectedFile:null
            }
        },

        methods:{
            onFileSelected(e){
               this.selectedFile = e.target.files[0]
               this.fileName = e.target.files[0].name
            },


            async addOwners(){
                let data = new FormData();
                data.append("name" , this.name);
                data.append("about" , this.about);
                data.append("photo" , this.selectedFile  , this.selectedFile.name);

                let response = await this.$axios.$post("http://localhost:5000/api/owners" , data );
                this.owners.push(this.name);
            }      
        }
    }
</script>

<style scoped>

    .cart-wrapper{
        display: flex;
        width: 50%;
        border-radius: 4px ;
        border: 1px solid #eee;
        flex-direction: column;

    }

    .cart-input{
        width: 100%;
        box-sizing: border-box;
        padding: 7px;
    }

    .cart-wrapper-button{
        width: 100%;
        padding: 7px;
        background: blue;
        text-align: center ;
        color: #eee;
        font-size: 12px ;
        cursor: pointer;
    }

</style>>

