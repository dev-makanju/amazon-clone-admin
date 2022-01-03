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
                   <select class="select-button">
                       <option value="1">1</option>
                       <option value="2">2</option>
                   </select>
               </div>

               <!--owner dropdown-->
               <div class="cart-wrapper">
                   <label for="">Owner</label>
                   <select class="select-button">
                       <option value="1">1</option>
                       <option value="2">2</option>
                   </select>
               </div>

               <!--title dropdown-->
               <div class="cart-wrapper">
                   <label for="">Title</label>
                   <select class="select-button">
                       <option value="1">1</option>
                       <option value="2">2</option>
                   </select>
               </div>

               <!--price dropdown-->
               <div class="cart-wrapper">
                   <label for="">Price</label>
                   <select class="select-button">
                       <option value="1">1</option>
                       <option value="2">2</option>
                   </select>
               </div>

               <!--description dropdown-->
               <div class="cart-wrapper">
                   <label for="">Description</label>
                   <textarea 
                      placeholder="enter a description"
                      cols="30" 
                      rows="10"
                      style="width:100%">
                   </textarea>
               </div>

               <!--photo dropdown--> 
               <div class="cart-wrapper">
                   <label for="">Add Photo</label>
                      <label for="choosefile button">
                           <input type="file">
                           <p style="margin-top">name of the file</p>
                      </label>
               </div>

               <div class="button-wrapper">
                    <span class="button-click">Add product</span>
               </div>
         </div>


         <div class="product-wrapper">
             
         </div>
    </div>
</template>

<script>
    export default {
        //load data first
        async asyncData({ $axios }){ 
            try{
                let catigories =  $axios.$get("http://localhost:5000/api/cartigories");
                let owners = $axios.$get("http://localhost:5000/api/owners");

                const [ carResponse , ownerResponse ] = await Promise.all({
                     catigories,
                     owners
                });
                console.log(carResponse);
                console.log(ownerResponse)
                
                return {
                    catigories:carResponse.catigories,
                    owners:ownerResponse.owners
                }
            }catch(err){
                console.log(err)
            }
        }
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