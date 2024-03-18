<template>
  <div
    class="m-auto text-center grid gap-6 max-w-[30rem]"
    flat
  >
    <h1 class="text-5xl font-bold font-[Merriweather]">
      Create your account
    </h1>
    <h2 class="text-xl">
      Discover hidden gems in your social network
    </h2>

    <SocialComponent />

    <Divider
      align="center"
      type="solid"
    >
      <b class="text-gray-500">Or sign in with social email</b>
    </Divider>

    <SimpleComponent state="signup" />

    <p>
      Already have an account?
      <NuxtLink
        to="/login"
        class="font-bold link"
      >
        Sign in
      </NuxtLink>
    </p>

    <p class="text-gray-700 full-width font-[merriweather]">
      By clicking "Start mining" or signing up, you agree to the
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
        Data Privacy Policy</a>. You also agree to receive information and offers relevant to our
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
