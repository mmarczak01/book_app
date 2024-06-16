<template>
    <div class="text">
      <p v-if="bookLength === 1">One single book!</p>
      <p v-else-if="bookLength > 5">{{ bookLength }} books</p>
      <p v-else-if="bookLength <= 5 && bookLength > 1">Not too many of them...</p>
      <p v-else>No books...<br>Go get some books!</p>
    </div>
</template>
<script>
export default {
  name: 'BooksLengthMsg',
  props: {
    bookLength: {
      type: Number,
      required: true
    }
  }
}
</script>
