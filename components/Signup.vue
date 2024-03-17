<template>
  <div class="m-auto text-center grid gap-6 max-w-[30rem]" flat>
    <h1 class="text-5xl font-bold font-[Merriweather]">Create your account</h1>
      <h2 class="text-xl">Discover hidden gems in your social network</h2>

    <div class="grid gap-6">
      <oauth-button label="Continue with Google" icon="pi pi-google" class="w-full text-h6" size="large"
        source="google" />
      <oauth-button label="Continue with Microsoft" icon="pi pi-microsoft" class="w-full text-h6" size="large"
        source="azure" />
    </div>

    <Divider align="center" type="solid">
      <b class="text-gray-500">Or sign in with social email</b>
    </Divider>

    <div class="grid gap-6 w-full">
      <FloatLabel>
        <InputText v-model="email" filled class="w-full" :invalid="!isValidEmail(email)" label="Email" type="email" required />
        <label for="email">Email</label>
      </FloatLabel>
      <FloatLabel>
        <Password v-model="password" class="w-full" :input-style="{ 'min-width': '100%' }" toggleMask :invalid="!isValidPassword(password)" required>
          <template #header>
            <h6>Pick a password</h6>
          </template>
          <template #footer>
            <Divider />
            <p class="mt-2">Suggestions</p>
            <ul class="pl-2 ml-2 mt-0" style="line-height: 1.5">
              <li>At least one lowercase</li>
              <li>At least one uppercase</li>
              <li>At least one numeric</li>
              <li>Minimum 8 characters</li>
            </ul>
          </template>
        </Password>
        <label for="password">Password</label>
      </FloatLabel>
      <Button @click="signUp" :loading="isLoading" label="Start Mining" size="large" />
    </div>

    <p>
      Already have an account?
      <NuxtLink to="/login" class="font-bold link">Sign in</NuxtLink>
    </p>

    <p class="text-gray-700 text-left full-width font-[merriweather]">
      By clicking "Start mining" or signing up, you agree to the
      <a class="link" href="https://www.leadminer.io/terms-of-service" target="_blank" rel="noopener noreferrer">
        Terms of Service
      </a>
      and
      <a class="link" href="https://www.leadminer.io/data-privacy" target="_blank" rel="noopener noreferrer">
        Data Privacy Policy</a>. You also agree to receive information and offers relevant to our
      services via email.
    </p>
  </div>

  <div class="card flex justify-content-center">
    <Toast />
  </div>
</template>

<script setup lang="ts">
import { isValidEmail } from "~/helpers/email";
import { ref } from "vue";
import OauthButton from "~/components/OAuthButton.vue";
import { isValidPassword } from "~/helpers/password";

const toast = useToast();

const supabase = useSupabaseClient();

const email = ref("");
const password = ref("");
const isLoading = ref(false);

async function signUp() {
  isLoading.value = true;
  try {
    const { error } = await supabase.auth.signUp({
      email: email.value,
      password: password.value,
      options: {
        emailRedirectTo: `${window.location.origin}/dashboard`,
      },
    });
    if (error) {
      throw error;
    }
    toast.add({
      severity: 'success',
      summary: 'Success Message',
      detail: `We have sent a confirmation email to ${email.value}`,
      life: 3000
    });
  } catch (error) {
    if (error instanceof Error) {
      toast.add({
        severity: 'error',
        summary: 'Error Message',
        detail: `Failed to signup: ${error.message}`,
        life: 3000
      });
    }
  } finally {
    isLoading.value = false;
  }
}
</script>
