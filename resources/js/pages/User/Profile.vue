<script setup>
import Layout from "@/layouts/default.vue"
import toastr from "toastr"

import { useForm, usePage } from "@inertiajs/vue3";

const authUser = usePage().props.user;

const tab = ref("personal-info");

const profilefForm = ref(null);

const userDetails = useForm({
  first_name: authUser.first_name,
  last_name: authUser.last_name,
  email: authUser.email,
});

const submitProfile = () => {
  profilefForm?.value?.validate().then((res) => {
    const { valid: isValid } = res;
    if (isValid) {
      userDetails.patch(route(`profile.update`, authUser.id), {
        preserveState: true,
        preventScroll: true,
        only: ["data", "params", "errors"],
        onSuccess: () => {
          toastr.info("Record updated");
          
         
        },
      });
    }
  });
};

const countryList = [
  "USA",
  "Canada",
  "UK",
  "Denmark",
  "Germany",
  "Iceland",
  "Israel",
  "Mexico",
];

const languageList = [
  "English",
  "German",
  "French",
  "Spanish",
  "Portuguese",
  "Russian",
  "Korean",
];

const username = ref("");
const email = ref("");
const password = ref("");
const cPassword = ref("");
const twitterLink = ref("");
const facebookLink = ref("");
const googlePlusLink = ref("");
const linkedInLink = ref("");
const instagramLink = ref("");
const quoraLink = ref("");
const languages = ref([]);
const isPasswordVisible = ref(false);
const isCPasswordVisible = ref(false);
</script>

<script>
export default {
  name: "Staff",
  layout: Layout,
};
</script>

<template>
  <VTabs v-model="tab">
    <VTab value="personal-info"> Personal Info </VTab>
    <VTab value="account-details"> Account Details </VTab>
    <VTab value="social-links"> Social Links </VTab>
  </VTabs>

  <VCard flat>
    <VCardText>
      <VWindow v-model="tab" class="disable-tab-transition">
        <VWindowItem value="personal-info">
          <VForm
            @submit.prevent="submitProfile"
            ref="profilefForm"
            validate-on="submit"
            class="mt-2"
          >
            <VRow>
              <VCol md="6" cols="12">
                <VTextField
                  v-model="userDetails.first_name"
                  label="First name"
                />
              </VCol>

              <VCol md="6" cols="12">
                <VTextField v-model="userDetails.last_name" label="Last name" />
              </VCol>

              <VCol cols="12" md="6">
                <VSelect
                  v-model="country"
                  :items="countryList"
                  label="Country"
                />
              </VCol>

              <VCol cols="12" md="6">
                <VSelect
                  v-model="languages"
                  :items="languageList"
                  multiple
                  chips
                  clearable
                  label="Language"
                />
              </VCol>
              <VCol cols="12" md="6">
                <VTextField
                  v-model="birthDate"
                  label="Birth Date"
                  placeholder="YYYY-MM-DD"
                />
              </VCol>
              <VCol cols="12" md="6">
                <VTextField v-model="phoneNo" type="number" label="Phone No." />
              </VCol>
            </VRow>
            <VDivider />

            <VCardText class="d-flex gap-4">
              <VBtn type="submit">Submit</VBtn>
              <VBtn color="secondary" variant="tonal"> Cancel </VBtn>
            </VCardText>
          </VForm>
        </VWindowItem>

        <VWindowItem value="account-details">
          <VForm class="mt-2">
            <VRow>
              <VCol cols="12" md="6">
                <VTextField v-model="username" label="Username" />
              </VCol>

              <VCol cols="12" md="6">
                <VTextField
                  v-model="email"
                  label="Email"
                  suffix="@example.com"
                />
              </VCol>

              <VCol cols="12" md="6">
                <VTextField
                  v-model="password"
                  label="Password"
                  :type="isPasswordVisible ? 'text' : 'password'"
                  :append-inner-icon="
                    isPasswordVisible ? 'tabler-eye' : 'tabler-eye-off'
                  "
                  @click:append-inner="isPasswordVisible = !isPasswordVisible"
                />
              </VCol>

              <VCol cols="12" md="6">
                <VTextField
                  v-model="cPassword"
                  label="Confirm Password"
                  :type="isCPasswordVisible ? 'text' : 'password'"
                  :append-inner-icon="
                    isCPasswordVisible ? 'tabler-eye' : 'tabler-eye-off'
                  "
                  @click:append-inner="isCPasswordVisible = !isCPasswordVisible"
                />
              </VCol>
            </VRow>
          </VForm>
        </VWindowItem>

        <VWindowItem value="social-links">
          <VForm class="mt-2">
            <VRow>
              <VCol cols="12" md="6">
                <VTextField v-model="twitterLink" label="Twitter" />
              </VCol>
              <VCol cols="12" md="6">
                <VTextField v-model="facebookLink" label="Facebook" />
              </VCol>
              <VCol cols="12" md="6">
                <VTextField v-model="googlePlusLink" label="Google+" />
              </VCol>
              <VCol cols="12" md="6">
                <VTextField v-model="linkedInLink" label="LinkedIn" />
              </VCol>
              <VCol cols="12" md="6">
                <VTextField v-model="instagramLink" label="Instagram" />
              </VCol>
              <VCol cols="12" md="6">
                <VTextField v-model="quoraLink" label="Quora" />
              </VCol>
            </VRow>
          </VForm>
        </VWindowItem>
      </VWindow>
    </VCardText>
  </VCard>
</template>
