<template>
  <div class="product-add">
    <section class="py-5">
      <div class="container px-4 px-lg-5 mt-5">
        <div
          class="
            row
            gx-4 gx-lg-5
            row-cols-2 row-cols-md-3 row-cols-xl-2
            justify-content-center
          "
        >
          <div class="col-sm-12">
            <div class="card">
              <div class="card-header bg-info p-4 text-center">
                <h4>Add new product</h4>
              </div>
              <div class="card-body">
                <div class="needs-validation" novalidate>
                  <div class="row g-2">
                    <div v-if="!submitted">
                      <div class="col-12">
                        <label for="productName" class="form-label">Product Name</label>
                        <input
                          type="text"
                          class="form-control"
                          id="productName"
                          v-model="product.name"
                          placeholder=""
                          required
                        />
                        <div class="invalid-feedback">Valid name is required.</div>
                      </div>
                      <div class="col-12">
                        <label for="productPhoto" class="form-label">Product Photo</label>
                        <input
                          type="text"
                          class="form-control"
                          id="productPhoto"
                          v-model="product.photo"
                          placeholder=""
                          required
                        />
                        <div class="invalid-feedback">Valid photo path is required.</div>
                      </div>
                      <div class="col-12">
                        <label for="productPrice" class="form-label">Price</label>
                        <div class="input-group has-validation">
                          <span class="input-group-text">CAD</span>
                          <input
                            type="text"
                            class="form-control"
                            id="productPrice"
                            v-model.number="product.price"
                            placeholder=""
                            required
                          />
                          <div class="invalid-feedback">Price is required.</div>
                        </div>
                      </div>
                      <div class="col-12">
                        <label for="productDescription" class="form-label">Product Description</label>
                        <textarea
                          class="form-control"
                          id="productDescription"
                          v-model="product.description"
                          placeholder=""
                        ></textarea>
                        <div class="invalid-feedback">Valid description</div>
                      </div>
                      <div class="col-12">
                        <label for="productType" class="form-label">Product Type</label>
                        <select class="form-control" id="productType" placeholder="" v-model="product.type" required>
                          <option value="">Select</option>
                          <option value="Mobile">Mobile</option>
                          <option value="Laptop">Laptop</option>
                          <option value="Parfum">Parfum</option>
                          <option value="Other">Other</option>
                        </select>
                        <div class="invalid-feedback">Valid photo path is required.</div>
                      </div>
                      <button class="w-100 btn btn-secondary btn-lg mt-3" type="button" @click="saveProduct">Save</button>
                    </div>
                    <div v-else>
                      <div class="alert alert-success alert-dismissible fade show" role="alert">
                        <strong>You submitted successfully!</strong>
                        <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
                    </div>
                    <button class="w-100 btn btn-success btn-lg mt-3" type="button" @click="newProduct">New product </button>
                  </div>
                  <hr class="my-4">
                  </div>
                </div>
            </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
import ProductDataService from '@/services/ProductDataService'

export default {
  props: ['addInv'],
  data () {
    return {
      submitted: false,
      product: {
        name: '',
        photo: '',
        price: '',
        description: '',
        type: ''
      }
    }
  },
  methods: {
    saveProduct () {
      ProductDataService.create(this.product)
        .then(response => {
          this.product.id = response.data.id
          this.addInv(this.product)
        })
      this.submitted = true
    },
    newProduct () {
      this.product = {
        name: '',
        photo: '',
        price: '',
        description: '',
        type: ''
      }
      this.submitted = false
    }
  }
}
</script>
