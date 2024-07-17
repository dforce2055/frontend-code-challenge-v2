<script>
export default {
  data() {
    return {
      showForm: false,
      showPost: false,
      editMode: false,
      title: "",
      content: "",
      author: "",
      posts: [],
    };
  },
  computed: {
    hasPosts() {
      return this.posts?.length > 0
    },
    titleMessage() {
      return this.hasPosts ? 'Edit' : 'Create New Post'
    },
    currentPost() {
      return this.posts[0]
    }
  },
  methods: {
    cleanForm() {
      this.title = ""
      this.content = ""
      this.author = ""
    },

    onCreateNewPost() {
      if (this.hasPosts) return
      this.showForm = !this.showForm
    },

    onEditPost() {
      this.editMode = true
      this.showPost = false

      const post = this.posts[0]
      this.title = post.title
      this.content = post.content
      this.author = post.author

      this.showForm = true
    },

    onSaveNewPost() {
      if (this.title === "" || this.content === "" || this.author === "") {
        return alert("Please fill all fields")
      }

      this.posts = [{
        title: this.title,
        content: this.content,
        author: this.author
      }]

      // this.cleanForm()
      this.showForm = false
      this.showPost = true
      this.editMode = false
    },

    onDeletePost() {
      this.showPost = false
      this.cleanForm()
      this.posts = []
    }
  }
};
</script>

<template>
  <div class="mt-100 layout-column align-items-center justify-content-center">
    <h1>Blog Posts</h1>
    <div>
      <button data-testid="new-button" @click="onCreateNewPost">
        New Post
      </button>
    </div>

    <!-- use this code template. -->

    <div v-if="showForm" class="card flex layout-column px-30">
      <h2 class="text-center">{{ titleMessage }}</h2>
      <input data-testid="new-title" type="text" placeholder="Title" v-model="title"><br>
      <textarea data-testid="new-content" placeholder="Content" v-model="content"></textarea><br>
      <input data-testid="new-author" type="text" placeholder="Author" v-model="author"><br>
      <button data-testid="save-button" class="mx-auto" @click="onSaveNewPost">
        Save
      </button>
    </div>

    <div  class="flex layout-column align-items-center justify-content-center">
      <div v-if="showPost" class="card px-50">
        <h2 data-testid="title">Title : {{ currentPost?.title }}</h2>
        <p data-testid="content">Content : {{ currentPost?.content }}</p>
        <p data-testid="author">Author : {{ currentPost?.author }}</p>
      </div>
      <div>
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
