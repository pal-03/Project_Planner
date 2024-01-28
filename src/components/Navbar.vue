<template>
    <nav class="main-nav">
      <router-link :to="{ name: 'Home' }">Projects</router-link>
      <router-link :to="{ name: 'AddProject' }">Add a New Project</router-link>
    </nav>
  </template>
  
  <script>
  export default {
  
  }
  </script>
  
  <style>
    .main-nav {
      text-align: center;
      margin: 40px auto;
    }
    /* Technically the router-link tag becomes an anchor in the actual rendering   */
    .main-nav a{
      display: inline-block;
      text-decoration: none;
      margin: 0 10px;
      color: #999;
      font-size: 18px;
    }
    /* Adding styles when the link is active */
    a.router-link-active {  
      border-bottom: 2px solid #00ce89;
      padding-bottom: 4px;
    }
  </style>