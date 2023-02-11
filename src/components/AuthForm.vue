<script lang="ts" setup>
import { useAuthStore } from "@/stores/auth";
import { Ref } from "vue";
import { UserCredentials } from "@supabase/supabase-js";

const props = defineProps<{
  signUp: boolean;
  title: string;
}>();

const credentials: Ref<UserCredentials> = ref({
  email: "",
  fname: "",
  lname: "",
  password: "",
});

const router = useRouter();

const emailLoading = ref(false);
async function emailAuth() {
  emailLoading.value = true;
  const { supabase } = useAuthStore();
  const { user, error } = props.signUp
    ? await supabase.auth.signUp(credentials.value)
    : await supabase.auth.signIn(credentials.value);
  if (user) router.push("/");
  else if (error) {
    alert(error.message);
    emailLoading.value = false;
  }
}

const gitHubLoading = ref(false);
async function gitHubAuth() {
  gitHubLoading.value = true;
  const { supabase } = useAuthStore();
  const { user, error } = await supabase.auth.signIn(
    { provider: "github" },
    {
      redirectTo: `${window.location.origin}/callback`,
    }
  );
  if (user) router.push("/");
  else if (error) {
    alert(error.message);
    gitHubLoading.value = false;
  }
}

const googleLoading = ref(false);
async function googleAuth() {
  googleLoading.value = true;
  const { supabase } = useAuthStore();
  const { user, error } = await supabase.auth.signIn(
    { provider: "google" },
    {
      redirectTo: `${window.location.origin}/callback`,
    }
  );
  if (user) router.push("/");
  else if (error) {
    alert(error.message);
    googleLoading.value = false;
  }
}

const twitterLoading = ref(false);
async function twitterAuth() {
  twitterLoading.value = true;
  const { supabase } = useAuthStore();
  const { user, error } = await supabase.auth.signIn(
    { provider: "twitter" },
    {
      redirectTo: `${window.location.origin}/callback`,
    }
  );
  if (user) router.push("/");
  else if (error) {
    alert(error.message);
    twitterLoading.value = false;
  }
}

const facebookLoading = ref(false);
async function facebookAuth() {
  facebookLoading.value = true;
  const { supabase } = useAuthStore();
  const { user, error } = await supabase.auth.signIn(
    { provider: "facebook" },
    {
      redirectTo: `${window.location.origin}/callback`,
    }
  );
  if (user) router.push("/");
  else if (error) {
    alert(error.message);
    facebookLoading.value = false;
  }
}

const loading = computed(
  () =>
    gitHubLoading.value ||
    emailLoading.value ||
    googleLoading.value ||
    twitterLoading.value ||
    facebookLoading.value
);
</script>
<template>
  <div>
    <h2 class="title text-center">
      {{ title }}
    </h2>
    <form class="flex w-full flex-col items-start" @submit.prevent="emailAuth">
      <VLabel v-if="signUp" for="fname">First Name</VLabel>
      <VInput
        v-if="signUp" 
        required
        :disabled="loading"
        class="w-full"
        name="First name"
        id="fname"
        type="text"
        :placeholder="fnameholder"
        v-model="(credentials.fname as string)"
      />
      <VLabel v-if="signUp" for="lname">Last name</VLabel>
      <VInput
        v-if="signUp" 
        required
        :disabled="loading"
        class="w-full"
        name="lname"
        id="lname"
        type="text"
        :placeholder="lnamePlaceholder"
        v-model="(credentials.lname as string)"
      />
      <VLabel for="email">Email</VLabel>
      <VInput
        required
        :disabled="loading"
        class="w-full"
        name="email"
        id="email"
        type="email"
        :placeholder="emailPlaceholder"
        v-model="(credentials.email as string)"
      />
      <VLabel for="password">Password</VLabel>
      <VPasswordInput
        :disabled="loading"
        class="mb-4 w-full"
        name="password"
        id="password"
        :placeholder="passwordPlaceholder"
        v-model="(credentials.password as string)"
      />

      <VButton
        :loading="emailLoading"
        :disabled="loading"
        type="submit"
        class="bg-teal-700"
        >{{ signUp ? "Sign Up" : "Sign In" }}</VButton
      >
      <router-link
        v-if="!signUp"
        to="/forgotpassword"
        class="text-sm text-center font-bold"
        style="width: 100%; margin-top: 24px; font-family: 'Noto Sans'; font-style: normal; font-weight: 500; font-size: 13px; line-height: 18px; color: #322DF0;"
      >
        Forgot your password?
      </router-link>
      <router-link
        v-if="signUp"
        to=""
        class="text-sm text-center font-bold mt-6"
        style="width: 100%; font-family: 'Noto Sans'; font-style: normal; font-weight: 500; font-size: 13px; line-height: 18px;"
      >
        By clicking "Sign up" you agree to our <span style="color: #322DF0;">Terms & Privacy Policy</span>
      </router-link>
    </form>

    <slot name="actions" />
  </div>
</template>

<style>
.title {
  font-family: 'Noto Sans';
  font-style: normal;
  font-weight: 700;
  font-size: 23px;
  line-height: 31px;

  margin-top: 64px;
  color: #000000;

  opacity: 0.72;
}
</style>