<template>
  <v-app class="pozadina">
    <v-container fill-height fluid class="background">
      <v-row align="center" justify="center">
        <v-col align="center" justify="center" cols="12">
          <v-card class="card-border" width="600px" outlined>
            <v-card-title align="left">LOGIN</v-card-title>
            <v-card-subtitle align="left">
              Deer user, plz login
            </v-card-subtitle>
            <v-card-text class="card-text-border">
              <v-form v-model="valid">
                <v-text-field
                  v-model="email"
                  dense
                  label="Email"
                  clearble
                  type="text"
                  :rules="[rules.required, rules.email]"
                  outlined
                ></v-text-field>
                <v-text-field
                  v-model="password"
                  dense
                  label="Password"
                  clearble
                  :append-icon="showIcon ? 'mdi-eye' : 'mdi-eye-off'"
                  :rules="[rules.required, rules.min]"
                  :type="showIcon ? 'text' : 'password'"
                  outlined
                ></v-text-field>
              </v-form>
              <v-btn
                @click="openDialog"
                class="link-left"
                text
                x-small
                color="blue"
              >
                Forgot password?
              </v-btn>
            </v-card-text>
            <v-card-actions class="card-actions">
              <v-btn @click="login" :disabled="isButtonDisabled" outlined>
                OK
              </v-btn>
            </v-card-actions>
          </v-card>
          <v-dialog
            width="300px"
            outlined
            persistent
            v-model="passwordIssuesDialog"
          >
            <v-card class="card-border">
              <v-card-title>E-mail</v-card-title>
              <v-card-subtitle> Please enter you e-mail </v-card-subtitle>
              <v-card-text>
                <v-text-field
                  v-model="emailForPassword"
                  dense
                  label="Email"
                  clearble
                  type="text"
                  :rules="[rules.required, rules.email]"
                  outlined
                ></v-text-field>
              </v-card-text>
              <v-card-actions class="card-actions">
                <v-btn
                  class="btn-right-margin"
                  color="red darken-3"
                  outlined
                  text
                  small
                  @click="closeDialog"
                >
                  CLOSE
                </v-btn>
                <v-btn outlined text @click="resetPassword(emailForPassword)">
                  SEND
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-dialog>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
export default {
  name: "LoginView",
  components: {},
  watch: {
    valid: function (newVal, oldVal) {
      if (newVal != true) {
        this.isButtonDisabled = true;
      } else {
        this.isButtonDisabled = false;
      }
    },
  },
  data() {
    return {
      emailForPassword: null,
      passwordIssuesDialog: false,
      isButtonDisabled: false,
      valid: true,
      email: null,
      password: null,
      showIcon: false,
      rules: {
        required: (value) => !!value || "Required.",
        min: (v) => v?.length >= 6 || "Min 6 characters",
        email: (v) =>
          !v ||
          /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) ||
          "E-mail must be valid",
      },
    };
  },
  methods: {
    login() {
      let email = this.email;
      let password = this.password;
    },
  },
  created() {},
  mounted() {},
  destroyed() {},
};
</script>

<style scoped>
.pozadina {
  /* Lighter coral color with reduced RGB values */
  background-color: #e7f6fc;
}
</style>
