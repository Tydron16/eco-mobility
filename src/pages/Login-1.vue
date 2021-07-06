<template>
  <q-layout>
    <q-page-container>
      <q-page class="flex bg-image flex-center">
        <q-card
          v-bind:style="$q.screen.lt.sm ? { width: '80%' } : { width: '30%' }"
        >
          <q-card-section>
            <q-avatar size="103px" class="absolute-center shadow-4">
              <img src="profile.svg" />
            </q-avatar>
          </q-card-section>
          <q-card-section>
            <div class="text-center q-pt-lg">
              <div class="col text-h6 ellipsis">
                Effettua l'accesso
              </div>
            </div>
          </q-card-section>
          <q-card-section>
            <q-form class="q-gutter-md" @submit.prevent.stop="onSubmit">
              <q-input
                filled
                v-model="username"
                label="Username"
                :rules="[
                  val =>
                    (val && val.length > 0) || 'Perfavore inserisci un valore'
                ]"
                lazy-rules
              />

              <q-input
                type="password"
                filled
                v-model="password"
                label="Password"
                :rules="[
                  val =>
                    (val && val.length > 0) || 'Perfavore inserisci un valore'
                ]"
                lazy-rules
              />

              <div>
                <q-btn label="Login" type="Submit" color="primary" />
              </div>
            </q-form>
          </q-card-section>
        </q-card>
      </q-page>
    </q-page-container>
  </q-layout>
</template>

<script>
import router from "src/router";
export default {
  data() {
    return {
      username: "",
      password: ""
    };
  },

  methods: {
    onSubmit() {
      this.$router.push("/Dashboard1");
    }
  }
};
</script>

<style>
.bg-image {
  background-image: linear-gradient(135deg, #7028e4 0%, #e5b2ca 100%);
}
</style>
