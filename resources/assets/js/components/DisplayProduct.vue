<template>
    <div>
        <h1>Products</h1>

        <div class="row">
          <div class="col-md-10"></div>
          <div class="col-md-2">
            <router-link :to="{ name: 'CreateProduct' }" class="btn btn-primary">Create Product</router-link>
          </div>
        </div><br />

        <table class="table table-hover">
            <thead>
            <tr>
                <td>ID</td>
                <td>Product Name</td>
                <td>Product Price</td>
                <td>Product Quantity</td>
                <td>Product Size</td>
                <td>Actions</td>
            </tr>
            </thead>

            <tbody>
                <tr v-for="product in products">
                    <td>{{ product.id }}</td>
                    <td>{{ product.name }}</td>
                    <td>{{ product.price }}</td>
                    <td>{{ product.quantity }}</td>
                    <td>{{ product.size }}</td>
                    <td><router-link :to="{name: 'EditProduct', params: { id: product.id }}" class="btn btn-primary">Edit</router-link></td>
                    <td><button class="btn btn-danger" v-on:click="deleteProduct(product.id)">Delete</button></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

    export default {
        data(){
            return{
                products: []
            }
        },

        created: function()
        {
            this.fetchProducts();
        },

        methods: {
            fetchProducts()
            {
              let uri = 'http://localhost:8000/products';
              this.axios.get(uri).then((response) => {
                  this.products = response.data;
              });
            },
            deleteProducts(id)
            {
              let uri = `http://localhost:8000/products/${id}`;
              this.products.splice(id, 1);
              this.axios.delete(uri);
            }
        }
    }
</script>