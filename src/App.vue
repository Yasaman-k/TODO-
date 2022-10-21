<template>
  <div class="container" v-if="$route.name!=='NotFound'">
    <header>
      <div class="nav-link">
        <img src="./assets/img/icons8-todo-list-100.png" />
        <img src="./assets/img/futurama-bender-48.png"/>
        <router-link class="title2 removeUnderline" to="/">Home</router-link>
      </div>
      <router-link class="removeUnderline" v-if="$route.name==='Home'" to="/create-task">
        <h2 class="title2">
          Create Task
        </h2>
      </router-link>
    </header>
    <router-view name="home"></router-view>
    <router-view name="createTask"></router-view>
  </div>
  <router-view name="notFound" />
</template>

<style scoped>
.container {
  margin: 2rem auto 8rem auto;
  max-width: 70vw;
}

.nav-link {
  display: flex;
  align-items: center;
}

header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>

<script>
export default {
  mounted () {
    // console.log(this.$route);
    // console.log(this.$route.name);
  }
}
</script>
