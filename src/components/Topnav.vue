<template>
  <div class="topnav">
    <svg class="icon icon-menu" aria-hidden="true" @click="toggleAside">
      <use xlink:href="#icon-menu"></use>
    </svg>
    <router-link to="/" class="logo">
      <svg class="icon icon-song" aria-hidden="true">
        <use xlink:href="#icon-song"></use>
      </svg>
    </router-link>
    <ul class="menu">
      <li><router-link to="/doc/button">文档</router-link></li>
    </ul>
  </div>
</template>

<script lang="ts">
  import { inject, Ref } from 'vue'
  export default {
    setup(){
      const asideVisible = inject<Ref<boolean>>('asideVisible')
      const toggleAside = () => {
        console.log('toggle')
        asideVisible.value = !asideVisible.value
      }
      return { toggleAside }
    }
  }
</script>

<style lang="scss" scoped>
  .topnav {
    display: flex;
    padding: 16px;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    z-index: 20;
    justify-content: center;
    align-items: center;
    background: #fff;
    border-bottom: 1px solid #ddd;
    .icon-menu{
      width: 16px;
      height: 16px;
    }
    a.logo:hover {
      border-bottom: none;
    }
    > .logo {
      max-width: 6em;
      margin-right: auto;
      > .icon-song {
        width: 30px;
        height: 30px;
      }
    }
    > .menu {
      display: flex;
      white-space: nowrap;
      flex-wrap: nowrap;
      > li {
        margin: 0 1em;
      }
    }
    > .icon-menu {
      display: none;
    }
    @media (max-width: 500px){
      > .logo {
        margin: 0 auto;
      }
      > .menu {
        display: none;
      }
      > .icon-menu {
        display: block;
      }
    }
  }
</style>
