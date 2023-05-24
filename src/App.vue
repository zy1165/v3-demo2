<script setup>
import { RouterLink, RouterView } from 'vue-router'

</script>

<template>
  <section id="Max-box">
    <nav id="Top-nav">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav>
    <div id="cont">
      <RouterView />
    </div>
  </section>
</template>

<style lang="scss" scoped>
#Max-box {
  width: 100vw;
  height: 100vh;

  #Top-nav {
    position: fixed;
    z-index: 99;
    background: hsl(0, 0%, 80%);
    box-shadow: 0 1px 5px 1px #0f0f0f6e;

    a {
      margin: 8px 0;
      border-radius: 100px;
      color: white;
      font-weight: 600;
    }

  }

  #cont {
    width: 100%;
    // height: 120%;
    position: absolute;
    box-sizing: border-box;
    padding-top: 45px;

  }

}

nav {
  width: 100%;
  font-size: 18px;
  text-align: center;
  //  float: left;
  // margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
  background: hsla(160, 100%, 37%, 1);
}

nav a.router-link-exact-active:hover {
  // background-color: transparent;
  background-color: #34445C;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  /* border-left: 1px solid var(--color-border); */
}

nav a:first-of-type {
  border: 0;
}
</style>
