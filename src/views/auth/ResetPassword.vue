<script lang="ts" setup>
import { useAuthStore } from "@/stores/auth";
const router = useRouter();
const route = useRoute();

/* Parse the route hash into a dictionary so we can pick out the access_token provided */
const hashDictionary = {} as any;
// first remove the actual '#' character
const hash = route.hash.replace("#", "");
// split hash into key-value pairs
hash.split("&").forEach((item) => {
  // split 'key=value' into [key, value]
  const [key, value] = item.split("=");
  // add to results
  hashDictionary[key] = value;
});
const resetToken = hashDictionary.access_token;

const password = ref("");
const loading = ref(false);
async function onSubmit() {
  const { supabase } = useAuthStore();
  loading.value = true;
  const { error, data } = await supabase.auth.api.updateUser(resetToken, {
    password: password.value,
  });
  console.log(error, data);

  if (error) {
    alert(error.message);
  } else {
    alert("successfully reset password.");
    router.push("/");
  }
  loading.value = false;
}
</script>
<template>
  <AppTopBar :signUp="false" />
  <div class="text-center mt-16 flex flex-col w-full items-center">
    <h2 class="mb-4 text-2xl font-bold">Reset Password</h2>
    <p class="mb-4 text-sm text-slate-500">Choose a new password below</p>
    <form class="flex flex-col items-start" @submit.prevent="onSubmit">
      <VLabel for="password">Password</VLabel>
      <VPasswordInput
        :disabled="loading"
        class="w-full"
        name="password"
        id="password"
        placeholder="Choose your password"
        v-model="password"
      />
      <VButton
        :loading="loading"
        type="submit"
        class="bg-teal-700"
      >
        Reset
      </VButton>
    </form>
  </div>
</template>
