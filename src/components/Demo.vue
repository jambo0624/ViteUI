<template>
  <div class="demo">
    <h2>{{component.__sourceCodeTitle}}</h2>
    <div class="demo-component">
      <component :is="component"/>
    </div>
    <div class="demo-actions">
      <Button theme="text" v-if="codeVisible" @click="hideCode">隐藏源代码</Button>
      <Button theme="text" v-else @click="showCode">查看源代码</Button>
    </div>
    <div class="demo-code" v-if="codeVisible">
      <pre class="language-html" v-html="html"></pre>
    </div>
  </div>
</template>

<script lang="ts">
  import Button from "../lib/Button.vue"
  import 'prismjs'
  import 'prismjs/themes/prism.css'
  import { computed, ref } from 'vue'
  export default {
    name: 'Demo',
    props: {
      component: Object
    },
    components:{
      Button
    },
    setup(props){
      const html = computed(()=>{
        return Prism.highlight(props.component.__sourceCode, Prism.languages.html, 'html')
      })
      const codeVisible = ref(false)
      const hideCode = ()=> codeVisible.value = false
      const showCode = ()=> codeVisible.value = true
      const Prism = (window as any).Prism
      return { Prism, html, codeVisible, hideCode, showCode }
    }
  }
</script>

<style lang="scss" scoped>
  $border-color: #d9d9d9;
  .demo{
    border: 1px solid $border-color;
    margin: 16px 0 32px;

    >h2 {
      font-size: 20px;
      padding: 8px 16px;
      border-bottom: 1px solid $border-color;
    }

    &-component {
      padding: 16px;
    }

    &-actions {
      padding: 8px 16px;
      border-top: 1px dashed $border-color;
      border-bottom: none;
    }
    &-code {
      padding: 8px 16px;
      border-top: 1px dashed $border-color;
      > pre {
        line-height: 1.1;
        font-family: Consolas, 'Courier New', Courier, monospace;
        margin: 0;
      }
    }
  }
</style>
