<template>
    <div class="product-container">
         <div class="product-wrapper">
               
         </div>
         <div class="product-wrapper center">
               <!--Add a product-->
               <h2 style="text-align:center">Add a new project</h2>
               <!--cartigory dropdown-->
               <div class="cart-wrapper">
                   <label for="">Catigory</label>
                   <select class="select-button" v-model="categoryID">
                       <option value="1">bags</option>
                        <option value="2">kitchen utncils</option>
                   </select>
               </div>

               <!--owner dropdown-->
               <div class="cart-wrapper">
                   <label for="">Owner</label>
                   <select class="select-button" v-model="ownerID">
                       <option value="1">makanaki</option>
                       <option value="2">odenaki</option>
                   </select>
               </div>

               <!--title dropdown-->
               <div class="cart-wrapper">
                   <label for="">Title</label>
                   <input type="text"
                        v-model="title"
                        class="select-button">
               </div>

               <!--price dropdown-->
               <div class="cart-wrapper">
                   <label for="">Price</label>
                   <input type="text"
                        v-model="price"
                        class="select-button">
               </div>
               
               <!--price dropdown-->
               <div class="cart-wrapper">
                   <label for="">stock quantity</label>
                   <input type="text"
                        v-model="stockquantity"
                        class="select-button">
                </div>

                   
               <!--description dropdown-->
               <div class="cart-wrapper">
                   <label for="">Description</label>
                   <textarea 
                      placeholder="enter a description"
                      v-model="description"
                      cols="30" 
                      rows="10"
                      style="width:100%">
                   </textarea>
               </div>

               <!--photo dropdown--> 
               <div class="cart-wrapper">
                   <label for="">Add Photo</label>
                      <label for="choosefile button">
                           <input type="file" @change="onFileSelected">
                           <p style="margin-top">{{ fileName }}</p>
                      </label>
               </div>

               <div style="margin-top:20px" class="button-wrapper">
                    <span class="button-click" @click="onAddProduct">Add product</span>
               </div>
         </div>


         <div class="product-wrapper">
             
         </div>
    </div>
</template>

<script>
    export default {
        //load data first
        async asyncData({ $axios } ){ 
            try{
                let catigories =  $axios.$get("http://localhost:5000/api/cartigories");
                let owners = $axios.$get("http://localhost:5000/api/owners");

                const [ catResponse , ownerResponse ] = await Promise.all([
                     catigories , owners
                ]);

                console.log(catResponse);
                
                return {
                    catigories:catResponse.catigories,
                     owners:ownerResponse.owners
                }
            }catch(err){
                console.log(err)
            }
        },
        data(){
            return{
                categoryID: null,
                ownerID: null,
                title:"",
                price:0,
                description:"",
                selectedFile:null  ,
                stockquantity:1,
                fileName:""
            }
        },
        methods: {
            onFileSelected(e){
                this.selectedFile = e.target.files[0]
                this.fileName = e.target.files[0].name 
            },
            async onAddProduct(){
                let data = new FormData();
                data.append("title" , this.title);
                data.append("price" , this.price);
                data.append("description" , this.description);
                data.append("stockquantity" , this.stockquantity)
                data.append("ownerID" , this.ownerID);
                data.append("categoryID" , this.categoryID);
                data.append("photo" , this.selectedFile  , this.selectedFile.name);

                let result = await this.$axios.$post("http://localhost:5000/api/products" , data).then( () => {
                    this.$router.push("/");
                });
            }      
        },

    }
</script>

<style scoped>
.product-container{
    display: flex;
    flex-direction: row;
    height: 100vh;
}

.product-wrapper{
    flex: 1 1 auto;
    order: 1;
    background: grey;
    height: 100% ;
    margin: 10px ;
}

.product-wrapper.center{
    width: 40%;
    padding: 10px;
}

.select-button{
    width: 100%;
    padding: 7px;
    border: 1px solid #eee;
}

.button-click{
    width: 100%;
    background: #fff;
    padding: 7px;
}
</style>