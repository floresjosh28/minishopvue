<template>
    <div>
        <h1>Update Product</h1>
        <div class="row">
          <div class="col-md-10"></div>
          <div class="col-md-2"><router-link :to="{ name: 'DisplayProduct' }" class="btn btn-success">Return to Products</router-link></div>
        </div>

        <form v-on:submit.prevent="updateProduct">
            <div class="form-group">
                <label>Product Name</label>
                <input type="text" class="form-control" v-model="product.name">
            </div>

            <div class="form-group">
                <label name="product_price">Product Price</label>
                <input type="text" class="form-control" v-model="product.price">
            </div>

            <div class="form-group">
                <label name="product_quantity">Product Quantity</label>
                <input type="text" class="form-control" v-model="product.quantity">
            </div>

            <div class="form-group">
                <label name="product_size">Product Size</label>
                <input type="text" class="form-control" v-model="product.size">
            </div>

            <div class="form-group">
                <button class="btn btn-primary">Update</button>
            </div>
        </form>
    </div>
</template>

<script>

    export default{
        data(){
            return{
                product:{}
            }
        },

        created: function(){
            this.getProduct();
        },

        methods: {
            getProduct()
            {
              let uri = `http://localhost:8000/products/${this.$route.params.id}/edit`;
                this.axios.get(uri).then((response) => {
                    this.product = response.data;
                });
            },

            updateProduct()
            {
              let uri = 'http://localhost:8000/products/'+this.$route.params.id;
                this.axios.patch(uri, this.product).then((response) => {
                  this.$router.push({name: 'DisplayProduct'});
                });
            }
        }
    }
</script>