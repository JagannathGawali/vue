<template>
  <tr>
    <td>
      <h2>
        Book List
        <button href="#/add-book" @click.stop="details">(Add Book)</button>
      </h2>
      <table striped hover :items="books" :fields="fields">
        <template slot="actions" scope="row">
          <b-btn size="sm" @click.stop="details(row.item)">Details</b-btn>
        </template>
      </table>
      <ul v-if="errors && errors.length">
        <li v-for="error of errors">
          {{error.message}}
        </li>
      </ul>
    </td>
  </tr>
</template>

<script>

import axios from 'axios'

export default {
  name: 'BookList',
  data () {
    return {
      fields: {
        isbn: { label: 'ISBN', sortable: true, 'class': 'text-center' },
        title: { label: 'Book Title', sortable: true },
        actions: { label: 'Action', 'class': 'text-center' }
      },
      books: [],
      errors: []
    }
  },
  created () {
    axios.get(`http://localhost:3000/book`)
    .then(response => {
	console.log(response);
      	console.log(response.data);
	this.books = response.data
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  methods: {
    details (evt) {

      evt.preventDefault()
      axios.post(`http://localhost:3000/book`, {"isbn":123,"title":"bfvhj"})
      .then(response => {
        console.log(response)
      })
      .catch(e => {
        this.errors.push(e)
      })
    
    }
  }
}
</script>
