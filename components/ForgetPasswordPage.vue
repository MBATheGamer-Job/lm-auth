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
          filled
          class="w-full"
          label="Email"
          type="email"
        />
        <label for="email">Email</label>
      </FloatLabel>
      <Button
        type="submit"
        unelevated
        label="Send reset instructions"
        size="large"
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
</template>
