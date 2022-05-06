<template>
  <main class="main">
    <SignupForm />
  </main>
</template>

<script>
import SignupForm from "./components/SignupForm.vue";
export default {
  name: "App",
  components: { SignupForm },
};
</script>

<style>
#app {
  height: 100%;
}
.main {
  display: flex;
  justify-content: center;
  align-items: center;

  height: 100%;
  max-width: 960px;

  margin: auto;
}
</style>
