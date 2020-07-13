<template>
  <div class="container py-5">
    <form @submit.stop.prevent="handleSubmit">
      <div class="form-group">
        <label for="name">Name</label>
        <input
          id="name"
          v-model="User.name"
          type="text"
          name="name"
          class="form-control"
          placeholder="Enter Name"
          required
        >
      </div>

      <div class="form-group">
        <label for="image">Image</label>
        <img
        v-if="User.image"
        :src="User.image"
        class="d-block img-thumbnail mb-3"
        width="200"
        height="200"
      />
        <input
          id="image"
          type="file"
          name="image"
          accept="image/*"
          class="form-control-file"
          @change="handleFileChange"
        >
      </div>

      <button
        type="submit"
        class="btn btn-primary"
      >
        Submit
      </button>
    </form>
  </div>
</template>

<script>

const dummyData = {
  'User': {
    'id': 1,
    'name': 'root',
    'email': 'root@example.com',
    'password': '$2a$10$OJ3jR93XlEMrQtYMWOIQh.EINWgaRFTXkd0Xi5OC/Vz4maztUXEPe',
    'isAdmin': true,
    'image': 'https://i.imgur.com/58ImzMM.png',
    'createdAt': '2019-07-30T16:24:54.983Z',
    'updatedAt': '2019-08-01T10:33:51.095Z',
  }
}

export default {
  data () {
    return {
      User: {
        'id': -1,
        'name': '',
        'image': ''
      }
    }
  },
  created () {
    const { id } = this.$route.params
    this.fetchUser(id)
  },
  methods: {
    fetchUser (UserId) {
      console.log('fetchUser id:', UserId)
      const { User } = dummyData
      this.User = {
        ...this.User,
        id: User.id,
        name: User.name,
        image: User.image
      }
    },
     handleFileChange(e) {
      // const files = e.target.files; // = filefist
      const {files} = e.target
      console.log("files", files);
      if (files.length === 0) {
        // 使用者沒有選擇上傳的檔案
        this.restaurant.image = "";
      } else {
        // 否則產生預覽圖
        const imageURL = window.URL.createObjectURL(files[0]);
        this.restaurant.image = imageURL;
      }
    },
    handleSubmit (e) {
      const form = e.target; // <form></form>
      const formData = new FormData(form);
      this.$emit('after-submit', formData)
    }
  }
}
</script>