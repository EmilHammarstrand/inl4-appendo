<template>

    <div class="home">

          <div class="background-image">
                <h1>Glued to your computer during break? AppenDo helps you break FREE</h1>
                <button class="btn btn-primary">Get started</button>

          </div>

    <b-button variant="info">......</b-button>

    </div>


<!--example of the list -->


</template>

<script>

import Vue from 'vue';
import { BootstrapVue, IconsPlugin  } from 'bootstrap-vue';
import { ButtonGroupPlugin } from 'bootstrap-vue';

Vue.use(ButtonGroupPlugin);
Vue.use(BootstrapVue);
Vue.use(IconsPlugin);

export default {
    name: 'Home'

}
</script>

<style scoped>

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