<template>

    <div class="home">

          <div class="background-image">
                <h1>Glued to your computer during break? AppenDo helps you break FREE</h1>
                <button class="btn">Get started</button>
          </div>


    </div>


<!--example of the list -->


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


/*
.container {
  position: relative;
  width: 100%;
  height: 100%;


}
*/

.home {

  height: 100%;
  width: 100%;
}

.background-image {


  background-size: cover;
  background-image: url(./images/nature-pic.jpg);
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