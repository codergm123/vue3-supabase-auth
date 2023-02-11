<script lang="ts" setup></script>
<template>
  <AppTopBar :signUp="true" />
  <div class="liquid-cheese flex h-full min-h-full" style="background: #F5F5F5;">
    <div class="mx-auto max-h-full rounded-lg">
      <div class="flex flex-col items-start">
        <AuthForm
          :sign-up="true"
          title="Create an account"
        >
          <template v-slot:actions>
            <div class="text-sm mt-6 mb-10" style="width: 100%; text-align: center;">
              <span style="font-family: 'Noto Sans'; font-style: normal; font-weight: 500; font-size: 15px; line-height: 20px; color: #000000; opacity: 0.64;">
                Already have an account?
              </span>
              <router-link to="/signin" class="font-bold" style="margin-left: 4px; font-family: 'Noto Sans'; font-style: normal; font-weight: 600; font-size: 15px; line-height: 20px; color: #322DF0;">
                Log in
              </router-link>
            </div>
          </template>
        </AuthForm>
      </div>
    </div>
  </div>
  <AppFooter />
</template>

