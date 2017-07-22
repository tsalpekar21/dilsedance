<template>
  <div id="app">
    <nav class="navbar">
      <div class="nav-brand">
        <img class="logo" src="~assets/logo.jpg"></img>
      </div>
      <div class="nav-container">
<!--         <a href="#" @click="toTestimonials($event, 'testimonials')" class="nav-title">
          Testimonials
        </a>
 -->        <a href="#" @click="toTestimonials($event, 'classes')" class="nav-title">
          Classes
        </a>
<!--         <a href="#" @click="toTestimonials($event, 'mission')" class="nav-title">
          Mission
        </a>
 -->        <a href="#" @click="toTestimonials($event, 'services')" class="nav-title">
          Services
        </a>
        <a href="#" @click="toTestimonials($event, 'contact')" class="nav-title">
          Contact
        </a>
      </div>
    </nav>
    <router-view></router-view>
  </div>
</template>

<script>
import './stylesheets/app.scss'
import velocity from 'velocity-animate'

export default {
  name: 'app',
  methods: {
    toTestimonials (e, section) {
      let el = document.querySelector('#' + section)
      velocity(el, 'scroll', { offset: '-70', easing: 'ease', duration: 800 })
    }
  }
}
</script>

<style lang='scss' scoped>
@import "./stylesheets/_vars.scss";

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // color: #2c3e50;
  // background: #B4B4B4;
  width: 100%;
  height: 100%;
}

.logo {
  position: relative;
  height: 100%;
  width: 140px;
  display: none;
}

.navbar {
  height: 60px;
  background: transparent;
  width: 100%;
  color: #000 !important;
  z-index: 500;
  position: fixed;
  transition: background .3s ease, box-shadow .3s ease;
  box-shadow: 0;

  .logo {
    animation-name: fadeOut;
    animation-iteration-count: 1;
    animation-timing-function: ease;
    animation-duration: .3s;
    animation-fill-mode:forwards;
  }

  &.transition {
    background: #ffffff;
    box-shadow: 0 10px 20px 0 rgba(0,0,0,.08);
    a {
      transition: color .3s ease-in-out;
      color: #004e67 !important;
    }

    .logo {
      display: block;
      animation-name: fadeIn;
      animation-iteration-count: 1;
      animation-timing-function: ease;
      animation-duration: .3s;
      animation-fill-mode:forwards;
    }
  }

  .nav-brand {
    position: absolute;
    height: 70px;
    display: inline-block;
    float: left;
    margin-left: 15px;
  }

  .nav-title {
    display: inline-block;
    z-index: 20;
    line-height: 60px;
    margin-right: 10px;
    margin-left: 10px;
    color: #ffffff !important;
  }

  .nav-container {
    text-align: right;
    z-index: 100;
    margin-right: 15px;
  }
}
</style>
