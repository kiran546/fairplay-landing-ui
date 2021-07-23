<template>
  <div style="background-image:url('@/static/Blackbg.png')">
    <v-app>
      <div>
        <img src="@/static/itstimeforyou.png" alt="player_img" />
      </div>
      <div>
        <img src="@/static/particals.png" alt="player_img" />
      </div>
      <div>
        <img src="@/static/100bonus.png" alt="player_img" />
      </div>
      <div>
        <img src="@/static/sunilnarine.png" alt="player_img" />
      </div>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-2 pa-4 landing">
              <div class="title">
                <v-card-title>
                  <div class="heading font-12">
                    <div>ENTER YOUR DETAILS</div>
                    <span>TO GET THE LINK</span>
                  </div>
                </v-card-title>
              </div>
              <v-card-text>
                <v-form v-model="isValid" ref="form" >
                  <v-label>Mobile Number</v-label>
                  <v-text-field
                    name="number"
                    label="Mobile Number"
                    v-model="number"
                    type="number"
                    :rules="numberRules"
                    id="number"
                    outlined
                    dense
                    @input="$v.number.$touch()"
                  ></v-text-field>

                  <v-label>Email ID</v-label>
                  <v-text-field
                    name="email"
                    label="Email ID"
                    v-model="email"
                    :rules="emailRules"
                    id="email"
                    type="text"
                    outlined
                    dense
                    @input="$v.email.$touch()"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer />
                <v-btn
                  v-on:keyup.enter="readyToPlay()"
                  @click="readyToPlay()"
                  class="bg-orange text-white"
                  color="warning"
                  >READY TO PLAY</v-btn
                >
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-app>
  </div>
</template>
<script>
import {
  required,
  minLength,
  between,
  email,
  number,
} from "vuelidate/lib/validators";
export default {
  components: {},
  data: () => {
    return {
      number: "",
      email: "",
      isValid: false,
      numberRules: [
        (v) => !!v || "Mobile Number is required",
        (v) => (v && v.length == 10) || "Mobile Number must contain 10 digits",
      ],
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) =>
          /^(([^<>()[\]\\.,;:\s@']+(\.[^<>()\\[\]\\.,;:\s@']+)*)|('.+'))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
            v
          ) || "E-mail must be valid",
      ],
    };
  },

  validations: {
    number: {
      required,
      minLength: minLength(10),
    },
    email: {
      required,
    },
  },
  computed: {
    //   emailErrors() {
    //     const errors = [];
    //     if (!this.$v.email.$dirty) return errors;
    //     !this.$v.email.required && errors.push("E-mail is required");
    //     return errors;
    //   },
    //  numberErrors() {
    //       const errors = []
    //       if (!this.$v.number.$dirty) return errors
    //       !this.$v.number.required && errors.push('Mobile No is required')
    //       return errors
    //     },
  },

  methods: {
    successToastr() {
      this.$toastr.Add({
        name: "Fairplay Landing",
        title: "Success!",
        msg: this.msg,
        clickClose: false,
        timeout: 2000,
        position: "toast-top-right",
        type: "success",
      });
    },
    errorToastr() {
      this.$toastr.Add({
        name: "Fairplay Landing",
        title: "Error!",
        msg: "No credentials found",
        clickClose: false,
        timeout: 2000,
        position: "toast-top-right",
        type: "error",
      });
    },

    readyToPlay() {
      this.$v.$touch();
      if (this.$refs.form.validate()) {
        const data = {
          number: this.number,
          email: this.email,
        };
        console.log(data, "data");
        this.msg = "Thanks for submission";
        this.successToastr();
        this.$refs.form.reset();
      } else {
        console.log("please fill the form correctly");

        this.errorToastr();
      }
    },
    
  },
};
</script>

<style lang ="scss">
.theme--light .v-card {
  border: 2px solid rgb(245, 124, 80) !important;
}
img {
  height: 50%;
  width: 50%;
  overflow: hidden;
}



</style>