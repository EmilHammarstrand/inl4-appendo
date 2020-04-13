<template>

  <div class="home">




    <div class="container">

        <img src="./images/nature-pic.jpg" alt="galaxy" style="width:100%">
            <h1>Glued to your computer during break? AppenDo helps you break FREE</h1>
            <button class="btn">Button</button>
    </div>



  </div>





</template>



<script>

import Vue from 'vue'
import { BootstrapVue, IconsPlugin } from 'bootstrap-vue'

Vue.use(BootstrapVue)
Vue.use(IconsPlugin)

export default {
    name: 'Home'

}
</script>

<style scoped>


.container {
  position: relative;
  width: 100%;
  max-width: 400px;
}

.container img {
  width: 100%;
  height: auto;
}

.container .btn {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  background-color: #f1f1f1;
  color: black;
  font-size: 16px;
  padding: 16px 30px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  text-align: center;
}

.container .btn:hover {
  background-color: black;
  color: white;
}






</style>