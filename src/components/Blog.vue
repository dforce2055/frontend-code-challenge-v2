<template>
  <div class="mt-100 layout-column align-items-center justify-content-center">
    <h1>Blog Posts</h1>
    <div>
      <button data-testid="new-button">New Post</button>
    </div>

    <!-- use this code template.

    <div class="card flex layout-column px-30">
      <h2 class="text-center">Create New Post</h2>
      <input data-testid="new-title" type="text" placeholder="Title"><br>
      <textarea data-testid="new-content" placeholder="Content"></textarea><br>
      <input data-testid="new-author" type="text" placeholder="Author"><br>
      <button data-testid="save-button" class="mx-auto">Save</button>
    </div>

    <div class="flex layout-column align-items-center justify-content-center">
      <div class="card px-50">
        <h2 data-testid="title">Title : </h2>
        <p data-testid="content">Content : </p>
        <p data-testid="author">Author : </p>
      </div>
      <div>
        <button data-testid="edit-button">Edit</button>
        <button data-testid="delete-button">Delete</button>
      </div>
    </div> 

    -->
    
  </div>
</template>

<script>
export default {
  data() {
    return {
    };
  },
  methods: {

  }
};
</script>

<style scoped>
  
  h1 {
    font-size: 24px;
  }
  h2 {
    font-size: 20px;
  }
  input[type="text"],
  textarea {
    padding: 5px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  input[type="text"]:focus,
  textarea:focus {
    outline: none;
    border-color: dodgerblue;
  }
</style>
