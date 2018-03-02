<template>
<div class="container">

<div class="form-group">
  <label for="usr">Name:</label>
  <input type="text" class="form-control" id="usr" v-model="p.name">
</div>
<div class="form-group">
  <label for="pwd">Price$:</label>
  <input type="text" class="form-control" id="pwd" v-model="p.price">
</div>

<button type="button" @click="createproducts" class="btn btn-primary">Create new product</button>

<table class="table table-striped table-borders">
 <thead>
  <tr>
   <th>id</th>
   <th>Name</th>
   <th>Price</th>
   <th>createdAt</th>
   <th>UpdatedAt</th>
   <th>Actions</th>
  </tr>
 </thead>
  <tbody>
  <tr v-for="user_alias in mproducts.data">
  <td>{{user_alias._id}}</td>
  <td>{{user_alias.name}}</td>
  <td>{{user_alias.price}}</td>
  <td>{{user_alias.createdAt}}</td>
  <td>{{user_alias.updatedAt}}</td>
  <td><button type="button" class="btn btn-danger" @click="removing(user_alias._id)"><em class="fa fa-trash"></em></button></td>
  <td><button type="button" class="btn btn-success">Edit</button></td>
  <td
  </tr>
  </tbody>
 </table>
 </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'user',
  data () {
    return {
      mproducts: [],
      p: {
        name: '',
        price: ''
      }ssss
    }
  },
  created () {
    this.myproducts()
  },
  methods: {
    myproducts () {
      axios.get('http://localhost:3000/api/product/getProducts')
      .then((response) => {
        this.mproducts = response.data
        console.log(response)
      })
    },
    createproducts () {
      let newProduct = {
        name: this.p.name,
        price: this.p.price
      }
      console.log(newProduct)
      axios.post('http://localhost:3000/api/product/createProduct', newProduct)
      .then((response) => {
        this.mproducts = response.data
        console.log(response)
      })
      .catch((error) => {
        console.log(error)
      })
      window.location.reload()
    }
  },
  removing (id) {
    axios.delete('http://localhost:3000/api/product/deleteProduct/' + id)
    .then((response) => {
      console.log(response)
    })
    .catch((error) => {
      console.log(error)
    })
    window.location.reload()
  },

}

</script>
<style>

</style>
