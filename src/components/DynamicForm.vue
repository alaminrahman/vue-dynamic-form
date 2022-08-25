<template>
  <div class="container mt-4">
    <div class="card">
      <div class="card-body">

        <div v-for="item, index in form" :key="item">
          <h1>Item {{ index + 1 }}</h1>
          {{item}}
          <div class="row" >

            <div class="col-sm-5">
              <label for="name">Name</label>
              <input type="text" id="name" class="form-control" v-model="item.name" />
            </div>

            <div class="col-sm-5">
              <label for="name">Price</label>
              <input type="number" id="name" class="form-control" v-model="item.price"/>
            </div>

            <div class="col-md-2 pt-4">
              <button class="btn btn-danger btn-sm m-1" @click="removeItem(index)">x</button>
              <button class="btn btn-success btn-sm m-1" @click="addRow">+</button>
            </div>

          </div><!--End row-->
        </div> <!--End for-->

        <button class="btn btn-primary" @click="saveItem">Save</button>
        
        
      </div>

    </div>
    
  </div>
</template>

<script>

import axios from 'axios';
import { reactive } from 'vue';

export default {
  name: 'DynamicForm',

  setup(){
    const form = reactive([
      {name: '', price: 0}
    ])

    const addRow = () => {
      form.push({name:'', price: 0})
    }

    const removeItem = (index) => {
      if(form.length > 1) {
        form.splice(index, 1)
      }
    }

    const saveItem = () => {
      axios.post('/items', form).then( res => {
        console.log(res)
        console.log('saved')
      })
    }

    return {
      form,
      addRow,
      removeItem,
      saveItem,
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
