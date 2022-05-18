<template>
  <div class="main-nav">
    <router-link to="/">Home</router-link>
    <router-link to="add-project">Add</router-link>
  </div>
</template>

<style scoped>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #999;
  font-size: 18px;
}
a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>
