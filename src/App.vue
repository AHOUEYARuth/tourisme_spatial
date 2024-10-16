<template>
  <div class="app">
    <header :class="{scrolled: isScrolled}">
      <div class="container">
        <div class="content">
          <router-link to="/"><img src="/src/assets/shared/logo.svg" alt=""></router-link>
          <nav>
            <ul>
              <li><router-link active-class="active" to="/"><strong>00</strong> HOME</router-link></li>
              <li><router-link active-class="active" to="/destination"><strong>01</strong> DESTINATION</router-link>
              </li>
              <li><router-link active-class="active" to="/crew"><strong>02</strong> CREW</router-link></li>
              <li><router-link active-class="active" to="/technology"><strong>03</strong> TECHNOLOGY</router-link></li>
            </ul>
            <button class="menu" @click="displayMenu()"><img src="/src/assets/shared/icon-hamburger.svg" alt=""
                :class="{ hide: display }"></button>
          </nav>
        </div>
      </div>
    </header>
    <main><router-view></router-view></main>
    <div class="menu_hide" :class="{ visible: display }">
      <button @click="displayMenu()"><img src="/src/assets/shared/icon-close.svg" alt=""></button>
      <nav>
        <ul>
          <li @click="displayMenu()"><router-link active-class="active" to="/"><strong>00</strong> HOME</router-link></li>
          <li @click="displayMenu()"><router-link active-class="active" to="/destination"><strong>01</strong> DESTINATION</router-link></li>
          <li @click="displayMenu()"><router-link active-class="active" to="/crew"><strong>02</strong> CREW</router-link></li>
          <li @click="displayMenu()"><router-link active-class="active" to="/technology"><strong>03</strong> TECHNOLOGY</router-link></li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";

const display = ref(false)
const isScrolled = ref(false)
function scrollPage() {
  isScrolled.value = window.scrollY > 40
}
onMounted(()=>{
  window.addEventListener('scroll', scrollPage)
})
onUnmounted(()=>{
  window.removeEventListener('scroll', scrollPage)
})
function displayMenu() {
  display.value = !display.value
}
</script>


<style scoped>
.app {
  width: 100%;
  padding: 0;
  margin: 0;
}

header {
  width: 100%;
  padding: 0;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 10;
}
.scrolled{
  background-color: #000000c5;
}
.container {
  max-width: 1044px;
  margin: 0 auto;
}

.content {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px 0;
  color: #fff;
}

.content a img {
  width: 70%;
}
ul {
  display: flex;
  align-items: center;
  gap: 40px;
}

li {
  list-style: none;
}

.active {
  border-bottom: 2px solid #fff;
  bottom: 10px;
}

.content li a {
  display: flex;
  align-items: center;
  gap: 10px;
  color: #ffffffcc;
}

.content li a strong {
  color: #fff;
}

.menu {
  background-color: inherit;
  border: none;
  display: none;
}

button {
  background-color: inherit;
  border: none;
  cursor: pointer;
}

.menu_hide {
  background-color: #000;
  color: #fff;
  width: 200px;
  padding: 20px;
  position: absolute;
  top: 10px;
  right: 0;
  display: flex;
  flex-direction: column;
  gap: 20px;
  display: none;
}

.menu_hide button {
  width: 100%;
  display: flex;
  justify-content: end;

}

.menu_hide nav {
  width: 100%;
}

.menu_hide nav ul {
  display: flex;
  flex-direction: column;
  width: 100%;
  padding: 0;
  align-items: start;
  gap: 30px;
}

.visible {
  display: block;
}

@media screen and (max-width: 1024px) {
  body {
    width: 100%;
  }

  .header {
    width: 100%;
  }

  .container {
    max-width: 80%;
  }
}

@media screen and (max-width: 768px) {
  body {
    width: 100%;
  }

  .header {
    width: 100%;
  }

  .container {
    max-width: 80%;
  }

  .content a img {
    width: 80%;
  }

  ul {
    gap: 20px;
  }
}

@media screen and (max-width: 375px) {
  .app {
    width: 100%;
  }

  .header {
    width: 100%;
  }

  .container {
    max-width: 80%;
  }

  nav ul {
    display: none;
  }

  .menu {
    display: flex;
  }

  .hide {
    display: none;
  }
}
</style>
