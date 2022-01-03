<template>
     <main>
         <div class="a-spacing-large">
               <div class="container-fluid  browsing-history">
                    <div class="row">
                         <div class="colum-sm-8 col-8">
                              <h1 class="a-size-large a-spacing-none a-text-normal">All Products</h1>
                               <!---BUTTONS-->
                               <a href="#" class="a-button-buy-again">Add a new product</a>
                               <a href="#" class="a-button-history margin-right-10">Add a new cartigory</a>
                               <a href="#" class="a-button-history margin-right-10">Add a new owner</a>
                               <!--LISTING PAGE-->
                         </div>
                    </div>
               </div>
         </div>
         
         <div v-for="(product , index ) in products" :key="product._id" class="container-fluid browsing-history">
              <div class="product-wrapper">
                    <div class="col-xl-2 col-lg-2 col-md-3 col-sn-6 br bb">
                           <div class="history-box">
                         <!--Product image-->
                         <a href="#" class="a-link-normal">
                              <img :src="product.photo" class="img-fluid" alt="images">
                         </a>
                         <!--Product title-->
                         <div class="a-spacing-top-base asin-title">
                              <span class="a-text-normal">
                                   <div class="p13n-sc-truncated">{{ product.title }}</div>
                              </span>
                         </div>
                         <!--Product rating-->
                         <div class="a-row">
                              <a href="#">
                                     <i class="fas fa-star"></i>
                                     <i class="fas fa-star"></i>
                                     <i class="fas fa-star"></i>
                                     <i class="fas fa-star"></i>
                                     <i class="fas fa-star"></i>
                              </a>

                              <span class="a-leter-space"></span>
                              <span class="a-color-tertiary a-size-small asin-reviews">Rating{{ product.rating}}</span>
                         </div>
                         <!--Product price-->
                         <div class="a-row">
                              <span class="a-size-base a-color-price">
                                    <span class="p13n-sc-price">{{ product.price }}</span>
                              </span>
                         </div>
                         <div class="a-row">
                              <a href="" class="a-button-history margin-right-10">update</a>
                              <a href="" class="a-button-history margin-right-10">delete</a>
                         </div>
                    </div>
                    </div>
              </div>
         </div>
     </main>
</template>

<script>
export default {
     name:"Tutorial",
     props:['products'],
};
</script>

<style>

.product-wrapper{
     box-shadow: 0px 2px 5px rgba(0 , 0 , 0 , .3);
     width: 20%;
     border-radius: 5px;
     padding: 3px;
}

</style>