<template>
  <div class="layout">
    <Topnav class="nav"/>
    <div class="content">
      <aside v-if="asideVisible">
        <h2>文档</h2>
        <ol>
          <li>
            <router-link to="/doc/intro">介绍</router-link>
          </li>
          <li>
            <router-link to="/doc/install">安装</router-link>
          </li>
          <li>
            <router-link to="/doc/get-started">开始使用</router-link>
          </li>
        </ol>
        <h2>组件列表</h2>
        <ol>
          <li>
            <router-link to="/doc/button">Button 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/dialog">Dialog 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/switch">Switch 组件</router-link>
          </li>
          <li>
            <router-link to="/doc/tabs">Tabs 组件</router-link>
          </li>
        </ol>
      </aside>
      <main>
        <router-view></router-view>
      </main>
    </div>
  </div>
</template>

<script lang="ts">
  import Topnav from '../components/Topnav.vue'
  import SwitchDemo from '../components/SwitchDemo.vue'
  import { inject, Ref, WatchEffect } from 'vue'
  export default {
    components: {
      Topnav,
      SwitchDemo
    },
    setup(){
      const asideVisible = inject<Ref<boolean>>('asideVisible')
      window.onresize= ()=>{
        if(document.body.clientWidth < 500){
          asideVisible.value = false
        }else {
          asideVisible.value = true
        }
      }
      return { asideVisible }
    }
  }
</script>

<style lang="scss" scoped>
  ol a:hover{
    border-bottom: none;
  }
  .layout{
    display: flex;
    flex-direction: column;
    height: 100vh;
    > .nav {
      flex-shrink: 0;
    }
    > .content {
      flex-grow: 1;
      padding-top: 60px;
      padding-left: 306px;
      @media (max-width:700px) {
        padding-left: 156px;
      }
      @media (max-width:500px) {
        padding-left: 0;
      }
    }
  }
  .content {
    display: flex;
    > aside {
      flex-shrink: 0;
    }
    > main {
      flex-grow: 1;
      padding: 16px;
    }
  }
  aside {
    border-right: 1px solid #f2f2f2;
    background: #fff;
    width: 250px;
    padding: 16px 0;
    position: fixed;
    top: 0;
    left: 0;
    padding-top: 77px;
    height: 100%;
    z-index: 1;
    @media (max-width: 700px) {
      width: 150px;
    }
    > h2 {
      margin-bottom: 4px;
      margin-top: 10px;
      padding: 0px 16px;
    }
    > ol {
      li {
        > a{
          display: block;
          padding: 4px 16px;
        }
        .router-link-active {
          background: #f6f8fa;
        }
      }
    }
  }
  main {
    overflow: auto;
  }
</style>

