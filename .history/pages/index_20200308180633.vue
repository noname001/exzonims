<template>
  <div class="container">
    <div>
      <logo />
      <h1 class="title">
        nuxt
      </h1>
      <h2 class="subtitle">
        My stunning Nuxt.js project
      </h2>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          class="button--green"
        >
          Fuck off
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
        {{data.total_count}}        
        </a>
      </div>
    </div>
    <el-input-number v-model="num" @change="handleChange" :min="1" :max="10"></el-input-number>
    <el-menu
      default-active="2"
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose"
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b">
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>{{first_item}}</span>
        </template>
        <el-menu-item-group title="Group One">
          <el-menu-item v-for="item in shit_submenu" :key="item" index="1-1">{{item}}</el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-menu-item v-for="training in sortCourses" v-bind:key="training.id">
        <i class="el-icon-menu"></i>
        <span>{{training.name}}</span>
      </el-menu-item>
      <el-menu-item index="3" disabled>
        <i class="el-icon-document"></i>
        <span>Navigator Three</span>
      </el-menu-item>
      <el-menu-item index="4">
        <i class="el-icon-setting"></i>
        <span>Navigator Four</span>
      </el-menu-item>
    </el-menu>
  </div>
  
</template>

<script>
import Logo from '~/components/Logo.vue'
import axios from 'axios'
import * as R from 'ramda'
import gql from 'graphql-tag';
// console.log(R.always('hello from Ramda')())
export default {
    data() {
      return {
        num: 1,
        first_item: "Shit",
        shit_submenu: ['substance', 'color' , 'weight'],
        data: {}
      };
    },
    methods: {
      handleChange(value) {
        console.log(value)
      },
      handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      // foo(){
      //   this.$apollo.query({query: `query {Course {name}}`, variables: {}})
      //   .then(({ data }) => {
      //     console.log(data)
      //     // do what you want with data
      //   })
      // }
    },
    asyncData (context) {
       let client = context.app.apolloProvider.defaultClient
       return client.query({query: gql`query {Course {id, name}}`, variables: {}})
        .then(({ data }) => {
          console.log(data)
          return data
          // do what you want with data
        })
        .catch(e=>console.log('catch block', e))
    //   var country = "france";
    //   axios.get(`https://api.github.com/search/users?q=${encodeURIComponent(`location:${country}`)}`)
    //           .then(res => res.json())
    //           .then(data => {
    //             return data
    //           })
    //           .catch(err => console.error(err));
    },
    computed: {
      sortCourses: function () {
        console.log(this.Course)
        return this.Course.filter((i)=>R.equals(85, parseInt(i.id)))
      },
    },
    // fetch(){
    //   // axios('http://localhost:3010/api')
    // },
    components: {
      Logo
    }
  };
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: left;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
