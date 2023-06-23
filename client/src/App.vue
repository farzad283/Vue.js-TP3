<template>
  <header class="d-flex justify-content-center py-3 bg-dark">
    <nav class="nav nav-pills">
      <router-link
        to="/"
        :class="`nav-link ${!activeLink ? 'active' : ''}`"
        @click="setActiveLink(!activeLink)"
      >
      Accueil
      </router-link>
      <router-link
        to="/about"
        :class="`nav-link ${activeLink ? 'active' : ''}`"
        @click="setActiveLink(!activeLink)"
      >
      Produits
      </router-link>
      <a
        href="https://github.com/farzad283/React.git"
        target="_blank"
        class="nav-link ml-4"
      >
        GitHub
      </a>
    </nav>
  </header>
  <RouterView
    :inventory="inventory"
    :addInv="addInventory"
    :updateInv="updateInventory"
    :removeInv = "removeInventory"
  />
  <footer class="py-5 bg-dark">
    <div class="container"><p class="m-0 text-center text-white">Copyright &copy; Your Website 2023</p></div>
  </footer>
</template>

<script>
// Move the import statement here
import 'bootstrap/dist/css/bootstrap.css'
import ProductDataService from '@/services/ProductDataService'
export default {
  data () {
    return {
      activeLink: false,
      inventory: []
    }
  },
  methods: {
    setActiveLink (value) {
      this.activeLink = value
    },
    addInventory (data) {
      this.inventory.push(data)
    },
    updateInventory (index, data) {
      this.inventory[index].name = data.name
      this.inventory[index].photo = data.photo
      this.inventory[index].price = data.price
      this.inventory[index].description = data.description
      this.inventory[index].type = data.type
    },
    removeInventory (index) {
      this.inventory.splice(index, 1)
    }
  },
  mounted () {
    ProductDataService.getAll()
      .then(response => {
        this.inventory = response.data
        console.log(this.inventory)
      })
  }
}
</script>
