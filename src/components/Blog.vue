<script setup>
import { ref, computed } from "vue"

const showForm = ref(false)
const showPost = ref(false)
const editMode = ref(false)
const title = ref("")
const content = ref("")
const author = ref("")
const posts = ref([])

const hasPosts = computed(() => posts.value.length > 0)
const titleMessage = computed(() => hasPosts.value ? 'Edit' : 'Create New Post')

const cleanForm = () => {
  title.value = ""
  content.value = ""
  author.value = ""
}

const onCreateNewPost = () => {
  if (hasPosts.value) return
  showForm.value = !showForm.value
}

const onEditPost = () => {
  editMode.value = true
  showPost.value = false

  const post = posts.value[0]
  title.value = post.title
  content.value = post.content
  author.value = post.author

  showForm.value = true
}

const onSaveNewPost = () => {
  if (title.value === "" || content.value === "" || author.value === "") {
    return alert("Please fill all fields")
  }

  posts.value = [{
    title: title.value,
    content: content.value,
    author: author.value
  }]

  cleanForm()
  showForm.value = false
  showPost.value = true
  editMode.value = false
}

const onDeletePost = () => {
  showPost.value = false
  cleanForm()
  posts.value = []
}

</script>
<template>
  <div class="mt-100 layout-column align-items-center justify-content-center">
    <h1>Blog Posts</h1>
    <div>
      <button
        data-testid="new-button" 
        @click="onCreateNewPost">
          New Post
        </button>
    </div>

    <!-- use this code template. -->

    <div 
      v-if="showForm" 
      class="card flex layout-column px-30"
    >
      <h2 class="text-center">{{ titleMessage }}</h2>
      <input data-testid="new-title" type="text" placeholder="Title" v-model="title"><br>
      <textarea data-testid="new-content" placeholder="Content" v-model="content"></textarea><br>
      <input data-testid="new-author" type="text" placeholder="Author" v-model="author"><br>
      <button 
        data-testid="save-button" 
        class="mx-auto"
        @click="onSaveNewPost">
          Save
      </button>
    </div>

    <div v-if="showPost" class="flex layout-column align-items-center justify-content-center">
      <div class="card px-50">
        <h2 data-testid="title">Title : {{ posts[0].title}}</h2>
        <p data-testid="content">Content : {{ posts[0].content }}</p>
        <p data-testid="author">Author : {{ posts[0].author }}ss</p>
      </div>
      <div v-if="hasPosts">
        <button data-testid="edit-button" @click="onEditPost">Edit</button>
        <button data-testid="delete-button" @click="onDeletePost">Delete</button>
      </div>
    </div> 

  </div>
</template>
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
