<template>
    <p>Books amount: {{ booksAmount }}</p>
    <p>Books price: {{ booksPrice }}</p>
</template>
<script>
export default {
  name: 'BooksSummary',
  props: {
    books: {
      type: Array,
      required: true
    }
  },
  computed: {
    booksAmount () {
      return this.books.length
    },
    booksPrice () {
      return this.books.reduce((sum, book) => sum + book.price, 0)
    }
  }
}
</script>
