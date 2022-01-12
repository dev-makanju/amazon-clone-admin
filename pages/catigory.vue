<template>
   <div class="cat-container">
        <h1>Add a cartigory</h1>
        <div class="cart-wrapper">
              <input type="text" class="cart-input" v-model="type">
              <hr/>
              <span class="cart-wrapper-button">
                  <span @click="addCart">Add cart</span>
            </span>
        </div>

        <ul  v-for="cartigory in cartigories"  :key="cartigory._id">
            <li>{{ cartigory.type }}</li>
        </ul>
   </div>
</template>

<script>
    export default {
        async asyncData({ $axios }){
            try{
                let response = await $axios.$get("http://localhost:5000/api/cartigories"); 
                return {
                    cartigories: response.categories
                }
            }catch(err){
                console.log(err);
            }
        },

        data(){
            return{
               type:""
            }
        },

        methods:{
            async addCart(){
                let data = { type: this.type }
                let response = await this.$axios.$post("http://localhost:5000/api/cartigories" , data );
                this.cartigories.push(data);
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
    }

</style>>

