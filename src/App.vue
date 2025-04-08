<template>
  <div class="w-full h-screen flex justify-center items-center bg-blue-200">
    <SignupForm />
  </div>
</template>

<script>
import SignupForm from './components/SignupForm.vue';


export default {
    name: 'App',
    components: {
        SignupForm
    }
    }
</script>


