<template>
    <div class="center-container">
        <p>
            Page
            <br />
            Not found
        </p>
        <router-link class="link" to="/">Back to home page ---></router-link>
    </div>
</template>

<style scoped>
.center-container {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.link {
    text-decoration: none;
    font-size: 30px;
    color: #966868;
}

p {
    font-size: 8rem;
    font-weight: 900;
    color: #966868;
}
</style>

<script>
export default {
  // created() {
  //     document.title = "404"
  // }
}
</script>
