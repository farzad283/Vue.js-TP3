<template>
  <div class="product-container">
    <section class="container px-4 px-lg-5 my-5">
        <div class="row gx-4 gx-lg-5 align-items-center">
            <div class="row gx-4 gx-lg-5 align-items-center">
                <div class="col-md-6">
                  <div class="image-container">
                    <div class="image-container">
                      <img class="card-img-top mb-5 mb-md-0" :src="`https://i.dummyjson.com/data/products/${product.id}/thumbnail.jpg`" :alt="product.name" />
                    </div>
                  </div>
                </div>
                <div class="col-md-6">
                    <div class="small mb-1">ID: {{ product.id }}</div>
                    <h1 class="display-5 fw-bolder">{{ product.name }}</h1>
                    <div class="fs-5 mb-2">
                        <span>{{ product.type }}</span>
                    </div>
                    <div class="fs-5 mb-2">
                        <strong>{{ product.price.toFixed(2) }}</strong>
                    </div>
                    <p class="lead">{{ product.description }}</p>
                </div>
            </div>
            <div class="d-flex justify-content-end mt-4">
                <router-link :to="{ name: 'edit-product', params: { id: product.id } }"  class="btn btn-primary">Edit Product</router-link>
            </div>
        </div>
    </section>
  </div>
</template>

<script>
export default {
  props: ['inventory', 'add'],
  computed: {
    product () {
      const productId = Number(this.$route.params.id)
      const product = this.inventory.find((p) => {
        return p.id === productId
      })
      console.log(product)
      console.log(this.inventory)
      console.log(this.$route.params.id)
      return product
    }
  }
}
</script>
<style>
.image-container {
  width: 500px; /* Adjust the width as desired */
  height: 500px; /* Adjust the height as desired */
  border-radius: 10px; /* Adjust the border radius as desired */
  overflow: hidden;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.product-container {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
