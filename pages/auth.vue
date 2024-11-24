<script setup lang="ts">
import { object, string, type InferType } from "yup";
import type { FormSubmitEvent } from "#ui/types";

const schema = object({
  email: string().email("Invalid email").required("Required"),
  password: string()
    .min(8, "Must be at least 8 characters")
    .required("Required"),
});

type Schema = InferType<typeof schema>;

const state = reactive({
  email: undefined,
  password: undefined,
});

async function onSubmit(event: FormSubmitEvent<Schema>) {
  console.log(event.data);
}
</script>
<template>
  <div
    class="flex flex-row justify-center mx-auto h-dvh items-center gap-[74px]"
  >
    <!-- right box -->

    <div
      class="bg-blue-500 w-[800px] h-[600px] rounded-3xl flex flex-col items-start justify-center px-16"
    >
      <h1 class="text-white text-5xl font-bold">Create.</h1>
      <h1 class="text-white text-5xl font-bold">Colloborate.</h1>
      <h1 class="text-white text-5xl font-bold">Build.</h1>
    </div>

    <!-- sign in and sign up forms  -->

    <div class="w-[415px] h-[px] p-6">
      <h3 class="text-xl font-manrope font-extrabold">Welocme to Website</h3>
      <UForm
        :schema="schema"
        :state="state"
        class="space-y-4"
        @submit="onSubmit"
      >
        <UFormGroup label="Email" name="email">
          <UInput v-model="state.email" />
        </UFormGroup>

        <UFormGroup label="Password" name="password">
          <UInput v-model="state.password" type="password" />
        </UFormGroup>

        <UButton block color="blue" type="submit" label="Submit" />

        <UButton variant="link" color="blue" label="Forgot Password?" />
      </UForm>
    </div>
  </div>
</template>
