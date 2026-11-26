<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue'
import header_svg from '../public/panel-top-24.svg?raw'
import nav_svg from '../public/panel-left-24.svg?raw'

const headerRef=ref(true)
const navRef=ref(true)

function hidden(value:any){
  const app=document.getElementById('app')
  if(!app) return
  if(value==='header'){
    if(headerRef.value===true){
      app.style.gridTemplateRows="40px 1fr"
      headerRef.value=false
    }else if(headerRef.value===false){
      app.style.gridTemplateRows="80px 1fr"
      headerRef.value=true
    }
  }else if(value==='nav'){
    if(navRef.value===true){
      app.style.gridTemplateColumns="0 1fr"
      navRef.value=false
    }else if(navRef.value===false){
      app.style.gridTemplateColumns="160px 1fr"
      navRef.value=true
    }
  }
}

</script>

<template>
  <span class="header-button" @click="hidden('header')">
    <svg width="24px" height="24px" aria-hidden="true" v-html="header_svg"></svg>
  </span>
  <span class="nav-button" @click="hidden('nav')">
    <svg width="24px" height="24px" aria-hidden="true" v-html="nav_svg"></svg>
    </span>
  <header>
    <p>这是顶栏</p>
  </header>
  <nav>
    <p>这是侧边栏</p>
    <RouterLink to="/">主页</RouterLink><br>
    <RouterLink to="/about">关于</RouterLink><br>
  </nav>
  <main id="main-scroll">
    <RouterView/>
  </main>
</template>

<style scoped>
  header,nav,main{
    box-sizing: border-box;
  }
  header{
    grid-area:header;
    border-bottom:1px solid #a3ee7a;
  }
  nav{
    grid-area:nav;
    overflow-y:auto;
    overflow-x:hidden;
    text-align: center;
    border-right:1px solid #a3ee7a;
  }
  main{
    grid-area:main;
    overflow:auto;
    padding:32px;
  }
  header > p{
    font-size:24px;
    text-align: center;
    color: #a3ee7a;
  }
  nav > p{
    font-size:16px;
    color: #ffabed;
  }
  .header-button{
    right:0;
  }
  .nav-button{
    left:0;
  }
  .header-button,.nav-button{
    transition: background-color 0.5s ease-in-out;
    border-radius:8px;
    padding:8px 8px 0 8px;
    position:absolute;
    top:0;
    cursor:pointer;
  }
  .header-button:hover,.nav-button:hover{
    background-color: rgba(0,0,0,0.1);
  }
</style>

<style>
  #app{
    margin:0;
    padding:0;
    max-height:none;
    height:100dvh;
    display:grid;
    grid-template-areas:
      "header header"
      "nav main";
    grid-template-rows:80px 1fr;
    grid-template-columns:160px 1fr;
    transition:grid 0.8s ease-in-out;
  }
  body{
    margin:0;
    padding:0;
    position:relative;
  }
</style>