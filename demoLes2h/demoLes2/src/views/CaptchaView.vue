<script lang="ts">
import Captcha from '@/components/Captcha.vue';
import { ref } from 'vue'

const showCaptcha = ref(true)
const isCaptchaCorrect = ref(false)

const processCaptcha = function(result : boolean){
  //console.log(`Captcha = ${result}`);
  isCaptchaCorrect.value = result;
  showCaptcha.value = false
}

</script>

<template>
    <div>
      <h1>captcha views</h1>
      <Captcha 
        v-if="showCaptcha"
        @correct="processCaptcha(true)" 
        @incorrect="processCaptcha(false)" 
        seconds="10"
      />

      <template v-else>
        <p v-if="isCaptchaCorrect">Welcome</p>
        <p v-else>No place for robots</p>
      </template>
      

    </div>
  </template>