<script lang="ts" setup>
const props = defineProps<{
  signUp: boolean;
}>();

</script>

<template>
  <header class="header z-12 bg-white">
    <div class="flex items-center justify-between mx-auto">
      <div class="flex items-center">
        <a class="textlogo font-logo md:text-md font-bold" href="/">
          __Logo__
        </a>
      </div>

      <div class="group relative dropdown text-purple-500 cursor-pointer text-base tracking-wide font-bold" style="fontFamily: 'none';">
        <span class="desc">
          {{signUp? "Already have an account?" : "Don't have an account yet?"}}
              
          <router-link v-if="signUp" to="/signin" class="signinbutton font-bold">
            Sign in
          </router-link>
          <router-link v-if="!signUp" to="/signup" class="signinbutton font-bold">
            Sign up
          </router-link> 
          
        </span>
      </div>
    </div>
  </header>
</template>

<style>
  .textlogo {
    font-family: 'Noto Sans'; 
    font-style: normal;
    font-weight: 700;
    color: #100F39; 
    font-size: 19px; 
    line-height: 26px; 
    margin-left: 24px; 
    margin-top: 24px; 
    margin-bottom: 22px;
  }

  .desc {
    font-family: 'Noto Sans';
    font-style: normal;
    font-weight: 500;
    font-size: 15px;
    line-height: 20px;
    color: #000000;
    opacity: 0.64;
    margin-right: 4px;
  }

  .signinbutton {
    font-family: 'Noto Sans'; 
    font-weight: 600;
    font-style: normal;
    color: #322DF0; 
    margin-right: 26px; 
    line-height: 20px; 
    font-size: 15px;
  }
</style>style>