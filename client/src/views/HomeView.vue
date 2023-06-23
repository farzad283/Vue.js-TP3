<template>
  <div className="container my-5">
    <nav class="navbar navbar-expand-lg navbar-light bg-light mb-4">
      <div class="container-fluid">
        <router-link
          :class="`btn btn-primary ${!activeLink ? 'active' : ''}`"
          aria-current="page"
          :to="{ name: 'add-product' }"
        >
          Add
        </router-link>
      </div>

    </nav>
    <section className="row row-cols-1 row-cols-md-3 mb-3 text-center">
      <div class="col mb-4" v-for="(product, index) in inventory" :key="index">
        <div class="card h-150 shadow-sm">
          <img class="bd-placeholder-img card-img-top" :src="`https://i.dummyjson.com/data/products/${product.id}/thumbnail.jpg`" alt="..." style="height: 270px;" />
          <div class="card-body">
            <div class="text-center">
              <h5 class="my-0 fw-normal">{{ product.name }}</h5>
              <h1 class="card-title pricing-card-title">${{ product.price }}</h1>
            </div>
          </div>
          <div class="card-footer p-4 pt-0 border-top-0 bg-transparent">
            <div class="text-center">
              <h5 class="my-0 fw-normal">{{ product.type }}</h5>
            </div>
          </div>
          <div class="card-footer p-4 pt-0 border-top-0 bg-transparent">
            <div class="text-center">
              <p>
                <router-link :to="{ name: 'product', params: { id: product.id } }">Details</router-link>
              </p>
            </div>
          </div>
        </div>
      </div>
    </section>
</div>
</template>

<script>
export default {
  props: ['inventory'],
  data () {
    return {
      activeLink: false
    }
  },
  methods: {
    setActiveLink (active) {
      this.activeLink = active
    }
  }
}
</script>
