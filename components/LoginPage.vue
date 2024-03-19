<template>
  <div
    class="m-auto text-center grid gap-6 max-w-[30rem]"
    flat
  >
    <h1 class="text-5xl font-bold font-[Merriweather]">
      Welcome back!
    </h1>
    
    <br>

    <SimpleComponent state="login" />

    <Divider
      align="center"
      type="solid"
    >
      <b class="text-gray-500">Or sign in with your email</b>
    </Divider>

    <SocialComponent />

    <p>
      Don't have an account?
      <NuxtLink
        to="/sign-up"
        class="font-bold link"
      >
        Sign up
      </NuxtLink>
    </p>

    <p class="text-gray-700 font-[merriweather]">
      By clicking "Start mining" or signing in, you agree to the
      <a
        class="link"
        href="https://www.leadminer.io/terms-of-service"
        target="_blank"
        rel="noopener noreferrer"
      >
        Terms of Service
      </a>
      and
      <a
        class="link"
        href="https://www.leadminer.io/data-privacy"
        target="_blank"
        rel="noopener noreferrer"
      >
        Data Privacy Policy </a>. You also agree to receive information and offers relevant to our
      services via email.
    </p>
  </div>

  <div class="card flex justify-content-center">
    <Toast />
  </div>
</template>

<script setup lang="ts">
import SimpleComponent from "./auth/SimpleComponent.vue";
import SocialComponent from "./auth/SocialComponent.vue";
</script>
