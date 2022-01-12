<template>
    <div class="product-container">
        <div class="product-wrapper">
               
        </div>
        <div class="product-wrapper center">
               <!--Add a product-->
               <h2 style="text-align:center">Update {{ product.title }}</h2>
               <!--cartigory dropdown-->
               <div class="cart-wrapper">
                   <label for="">Catigory</label>
                   <select class="select-button" v-model="categoryID">
                       <option v-for="cartigory in catigories" 
                       :value="cartigory._id" 
                       :key="cartigory._id" >
                           {{ cartigory.type }}
                       </option>
                   </select>
               </div>

               <!--owner dropdown-->
               <div class="cart-wrapper">
                   <label for="">Owner</label>
                   <select class="select-button" v-model="ownerID">
                       <option v-for="owner in owners" 
                        :value="owner._id" 
                        :key="owner._id">
                          {{ owner.name }}
                       </option>
                   </select>
               </div>

               <!--title dropdown-->
               <div class="cart-wrapper">
                   <label for="">Title</label>
                   <input type="text"
                        v-model="title"
                        class="select-button" :placeholder="product.title">
               </div>

               <!--price dropdown-->
               <div class="cart-wrapper">
                   <label for="">Price</label>
                   <input type="text"
                        v-model="price"
                        class="select-button" :placeholder="product.price">
               </div>
               
               <!--price dropdown-->
               <div class="cart-wrapper">
                   <label for="">stock quantity</label>
                   <input type="text"
                        v-model="stockquantity"
                        class="select-button" :placeholder="product.stockquantity" >
                </div>

                   
               <!--description dropdown-->
               <div class="cart-wrapper">
                   <label for="">Description</label>
                   <textarea 
                      :placeholder="product.description"
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
                    <span style="cursor:pointer" class="button-click" @click="onUpdatedProduct">update product</span>
               </div>
         </div>


         <div class="product-wrapper">
             
         </div>
    </div>
</template>

<script>
    export default {
        //load data first
        async asyncData({ $axios , params} ){ 
            try{
                let catigories =  $axios.$get("/api/cartigories");
                let owners = $axios.$get("/api/owners");
                let product = $axios.$get(`/api/products/${params.id}`);

                const [ catResponse , ownerResponse , productResponse] = await Promise.all([
                     catigories , owners , product
                ]);

                console.log(catigories)
                
                return {
                    catigories:catResponse.categories,
                    owners:ownerResponse.owners,
                    product:productResponse.product
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
                price:"",
                description:"",
                selectedFile:null  ,
                stockquantity:"",
                fileName:""
            }
        },
        methods: {
            onFileSelected(e){
                this.selectedFile = e.target.files[0]
                this.fileName = e.target.files[0].name 
            },
            async onUpdatedProduct(){
                let data = new FormData();
                data.append("title" , this.title);
                data.append("price" , this.price);
                data.append("description" , this.description);
                data.append("stockquantity" , this.stockquantity)
                data.append("ownerID" , this.ownerID);
                data.append("categoryID" , this.categoryID);
                data.append("photo" , this.selectedFile  , this.selectedFile.name);

                let result = await this.$axios.$put(`http://localhost:5000/api/products/${this.$route.params.id }` , data).then( () => {
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