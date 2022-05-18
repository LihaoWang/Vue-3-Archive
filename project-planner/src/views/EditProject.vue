<template>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input type="text" v-model="title" required />
    <label>Details</label>
    <textarea v-model="details" required></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  props: ['id'],
  data() {
    return {
      title: '',
      details: '',
    }
  },
  methods: {
    handleSubmit() {
      fetch(`http://localhost:3000/projects/${this.id}`, {
        method: 'PATCH',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          title: this.title,
          details: this.details,
        }),
      }).then(() => {
        this.$router.push('/')
      })
    },
  },
  mounted() {
    fetch(`http://localhost:3000/projects/${this.id}`)
      .then((res) => res.json())
      .then((res) => {
        this.title = res.title
        this.details = res.details
      })
  },
}
</script>

<style>
form {
  background: white;
  padding: 20px;
  border-radius: 10px;
}
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  width: 100%;
  box-sizing: border-box;
}
textarea {
  border: 1px solid #ddd;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
  height: 100px;
}
form button {
  display: block;
  margin: 20px auto 0;
  background: #00ce89;
  color: white;
  padding: 10px;
  border: 0;
  border-radius: 6px;
  font-size: 16px;
}
</style>
