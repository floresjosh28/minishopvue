<template>
  <div>
    <h1>Create A Product</h1>
    <form v-on:submit.prevent="addProduct">
      <div class="row">
        <div class="col-md-3">
          <div class="form-group">
            <label>Product Name:</label>
            <input type="text" class="form-control" v-model="product.name">
          </div>
        </div>
        </div>
        <div class="row">
          <div class="col-md-3">
            <div class="form-group">
              <label>Product Price:</label>
              <input type="text" class="form-control col-md-6" v-model="product.price" />
            </div>
          </div>
        </div><br />
        <div class="row">
          <div class="col-md-3">
            <div class="form-group">
              <label>Product Quantity:</label>
              <input type="text" class="form-control col-md-6" v-model="product.quantity" />
            </div>
          </div>
        </div><br />
        <div class="row">
          <div class="col-md-3">
            <div class="form-group">
              <label>Product Size:</label>
              <input type="text" class="form-control col-md-6" v-model="product.size" />
            </div>
          </div>
        </div><br />
        <div class="form-group">
          <button class="btn btn-primary">Add Product</button>
        </div>
    </form>
  </div>
</template>
<script>
  export default {
    data(){
        return{
          product:{}
        }
    },
    methods: {
      addProduct(){
        let uri = 'http://localhost:8000/products';
        this.axios.post(uri, this.product).then((response) => {
          this.$router.push({name: 'DisplayProduct'})
        })
    }
  }
}
</script>