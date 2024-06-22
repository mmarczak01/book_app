<template>
  <div id="app" class="app">
    <header class="app__heading">
      <h1>Books<span>.app</span></h1>
    </header>
    <books-list
      @remove="removeBook"
      :books="books" />
    <books-length-msg
      :bookLength="books.length" />
    <book-form
      @add="addBook" />
    <books-summary
    :books="books" />
  </div>
</template>
<script>
import BooksList from './components/BooksList'
import BooksLengthMsg from './components/BooksLengthMsg'
import BookForm from './components/BookForm'
import BooksSummary from './components/BooksSummary'
import axios from 'axios'
export default {
  name: 'App',
  data: () => ({
    books: []
  }),
  methods: {
    removeBook (index) {
      this.books.splice(index, 1)
    },
    addBook (book) {
      this.books.push({ ...book })
    },
    async fetchBooks () {
      try {
        const response = await axios.get('https://api.itbook.store/1.0/new')
        this.books = response.data.books.slice(0, 3).map(book => ({
          title: book.title,
          price: parseFloat(book.price.replace('$', ''))
        }))
      } catch (error) {
        console.error('Error fetching books:', error)
      }
    }
  },
  async created () {
    await this.fetchBooks()
  },
  components: {
    BooksList, BooksLengthMsg, BookForm, BooksSummary
  }
}
</script>
<style lang="scss">
.app {
  width: 100%;
  max-width: 1000px;
  padding: 2rem;
  margin: 0 auto;

  &__heading {
    font-size: 3rem;
    text-align: center;
    span {
      color: #5a58da;
    }
  }
}
</style>
