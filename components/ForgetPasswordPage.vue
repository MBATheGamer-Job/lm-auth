<template>
  <div
    class="m-auto text-center grid gap-6 max-w-[30rem]"
    flat
  >
    <h1 class="text-5xl font-bold font-[Merriweather]">
      Forgot your password?
    </h1>
    <h2 class="text-lg">
      Enter the email address associated with your account
    </h2>

    <form class="grid gap-4 w-full">
      <FloatLabel>
        <InputText
          v-model="email"
          filled
          class="w-full"
          label="Email"
          type="email"
        />
        <label for="email">Email</label>
      </FloatLabel>
      <ButtonComponent
        type="submit"
        label="Send reset instructions"
        size="large"
        @click="resetPassword"
      />
      <p>
        Back to
        <NuxtLink
          to="/login"
          class="font-bold link"
        >
          Sign in
        </NuxtLink>
      </p>
    </form>
  </div>

  <div class="card flex justify-content-center">
    <Toast />
  </div>
</template>

<script setup lang="ts">
import ButtonComponent from "./button/ButtonComponent.vue";
import { ref } from "vue";


const toast = useToast();

const supabase = useSupabaseClient();

const email = ref("");
const isLoading = ref(false);

async function resetPassword() {
  isLoading.value = true;
  try {
    const { error } = await supabase.auth.resetPasswordForEmail(email.value, {
      redirectTo: `${window.location.origin}/account`,
    });

    if (error) {
      throw error;
    }
    toast.add({
      severity: 'success',
      summary: 'Success Message',
      detail: "If an account exists with this email address, you will receive password reset instructions",
      life: 3000
    });
  } catch (error) {
    if (error instanceof Error) {
      toast.add({
        severity: "error",
        summary: "Error Message",
        detail: error.message,
        life: 3000,
      });
    }
  } finally {
    isLoading.value = false;
  }
}
</script>
