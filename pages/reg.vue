<template>
  <div>
    <div class="img">
      <AudioPlayer />

      <button class="signup-button" @click="toggleLogin">Sign up</button>
    </div>
    <div
      :class="{ 'login-container': true, 'show-login': isLoginVisible }"
      v-if="isLoginVisible"
    >
      <div class="reg-hero">
        <div class="hero-right">
          <div class="hero-right-content">
            <h3 class="hero-right-heading">
              Sathyam vada | dharmam chara
              <button class="play-btn">
                <img :src="require(`~/components/playbtn.png`)" />
              </button>
            </h3>
            <div class="hero-right-input-grp">
              <div class="input-grp" style="position: relative; top: -1vw">
                <input
                  type="text"
                  class="label"
                  placeholder="First name"
                  v-model="firstname"
                />
                <input
                  type="text"
                  class="label"
                  placeholder="Last name"
                  v-model="lastname"
                />
              </div>
              <div class="input-grp dob-grp">
                <input
                  type="email"
                  class="label"
                  placeholder="Email"
                  v-model="email"
                  style="
                    width: 16vw;
                    position: relative;

                    left: 0.4vw;
                  "
                />
                <input
                  type="date"
                  class="label dob"
                  placeholder="DOB"
                  v-model="dob"
                />
                <div class="hero-right-radio-grp">
                  <img
                    :src="require(`~/components/gender.png`)"
                    class="gender"
                  />
                  <div class="hero-right-radio-btn-grp">
                    <input type="radio" name="gender" id="" v-model="gender" />
                    <input type="radio" name="gender" id="" v-model="gender" />
                  </div>
                </div>
              </div>
              <div class="input-grp country-grp">
                <select
                  class="label"
                  v-model="country"
                  :items="countries"
                  @click="getCountryInfo"
                  style="position: relative; left: 0.5vw; width: 16.5vw"
                >
                  <option value="india" disabled></option>
                  <option
                    v-for="country in countries"
                    :key="country.id"
                    :value="country.name"
                  >
                    {{ country.name }}
                  </option>
                </select>

                <div class="country-dropdown">
                  <img
                    :src="getFlag(country)"
                    style="height: 5vh; width: 3vw"
                  />
                </div>
                <input
                  class="phone"
                  type="text"
                  v-model="phone"
                  :placeholder="getPhoneCode(country) + ' Ph no'"
                />
              </div>
              <div class="bottom-grp">
                <div class="input-grp">
                  <div class="ref-grp">
                    <img
                      :src="require(`~/components/lens.jpeg`)"
                      alt="icon"
                      style="
                        height: 20px;
                        position: relative !important;
                        left: 0vw;
                        top: -0.5vw !important;
                      "
                    />
                    <div class="ref-sub-grp">
                      <h6>Social media</h6>
                      <input
                        type="radio"
                        v-model="referencecategory"
                        value="socialmedia"
                      />
                    </div>
                    <div class="ref-sub-grp">
                      <h6>Reference</h6>
                      <input
                        type="radio"
                        v-model="referencecategory"
                        value="reference"
                      />
                    </div>
                    <div class="ref-sub-grp">
                      <h6>News</h6>
                      <input
                        type="radio"
                        v-model="referencecategory"
                        value="news"
                      />
                    </div>
                  </div>
                  <select
                    class="label"
                    v-model="language"
                    style="width: 16.5vw"
                  >
                    <option value="" disabled>selected Languages</option>
                    <option value="English">English</option>
                    <option value="Malayalam">Malayalam</option>
                    <option value="Tamil">Tamil</option>
                    <option value="Teluhu">Teluhu</option>
                    <option value="Kannada">Kannada</option>
                    <option value="Hindi">Hindi</option>
                  </select>
                </div>
                <div class="input-grp">
                  <input
                    type="text"
                    class="remarks"
                    v-model="comments"
                    placeholder="Special remarks"
                  />
                </div>
                <div class="submit">
                  <button @click="showDialogbox">Submit</button>

                  <!-- Dialog Box -->
                  <div
                    class="modal"
                    tabindex="-1"
                    role="dialog"
                    style="display: block"
                    v-if="showDialog"
                  >
                    <div class="modal-dialog" role="document">
                      <div class="modal-content">
                        <div class="modal-header">
                          <h5 class="modal-title">Enter You OTP</h5>
                        </div>
                        <div class="modal-body">
                          <div v-if="isOTPOpen">
                            <input
                              v-model="otp"
                              type="text"
                              placeholder="Enter OTP"
                            />
                          </div>
                        </div>
                        <div class="modal-footer">
                          <button
                            type="button"
                            class="btn-secondary"
                            @click="submitotp"
                          >
                            Submit
                          </button>
                          <!-- Add your submit functionality here -->
                          <button type="button" class="btn-secondary">
                            Resend
                          </button>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>

              <div class="hero-right-ribbon">
                <div class="ribbon-grp">
                  <h3>39997</h3>
                  <h4>Total meditators</h4>
                </div>
                <div class="ribbon-grp">
                  <h3>39997</h3>
                  <h4>Total meditators</h4>
                </div>
                <div class="ribbon-grp">
                  <h3>39997</h3>
                  <h4>Total meditators</h4>
                </div>
                <div class="ribbon-grp">
                  <h3>39997</h3>
                  <h4>Total meditators</h4>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="a">
      <div :class="{ 'image-background': isRedBackground }"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import AudioPlayer from "~/components/Audioplayer.vue";

export default {
  components: {
    AudioPlayer,
  },
  data() {
    return {
      isLoginVisible: false,
      isRedBackground: false,
      firstname: "",
      lastname: "",
      email: "",
      dob: "",
      gender: "",
      country: "india",
      countries: [],
      flag: [],
      digitalCode: [],
      phone: "",
      formattedPhoneNumber: "",
      referencecategory: "",
      language: "",
      comments: "",
      languagehome: "",
      isPlaying: false,
      showDialog: false,
      isOTPOpen: true, // Modify this based on your conditions
      otp: "",
    };
  },
  mounted() {
    this.getCountryInfo();
    if (this.showDialog) {
      this.requestOTP(); // Call the OTP request API when the component is mounted and the dialog box is open
    }
  },
  computed: {
    formattedPhoneNumber: {
      get() {
        return `${this.getPhoneCode(this.country)} ${this.phone}`;
      },
      set(value) {
        const code = this.getPhoneCode(this.country);
        const phone = value.replace(code + "").trim(); // removing the code from the input value
        this.phone = phone;
        console.log(phone);
      },
    },
  },
  methods: {
    toggleLogin() {
      this.isLoginVisible = !this.isLoginVisible;
      this.isRedBackground = !this.isRedBackground;
    },

    async getCountryInfo() {
      try {
        const response = await axios.get(
          "http://89.47.164.122:4000/api/registrations/countrieslist"
        );
        const countryData = response.data;
        this.countries = countryData;
        this.flags = countryData.map((country) => country.flag);
        this.digitalCodes = countryData.map((country) => country.phonecode);
        // console.log(this.countryNames);
        // console.log(this.flags);
        // console.log(this.digitalCodes);
      } catch (error) {
        console.error("Error fetching country information", error);
        throw error;
      }
    },

    getFlag(selectedCountry) {
      const index = this.countries.findIndex(
        (country) => country.name === selectedCountry
      );
      if (index !== -1 && this.flags && this.flags.length > index) {
        return this.flags[index];
      }
      return "";
    },

    getPhoneCode(selectedCountry) {
      const index = this.countries.findIndex(
        (country) => country.name === selectedCountry
      );
      if (
        index !== -1 &&
        this.digitalCodes &&
        this.digitalCodes.length > index
      ) {
        return this.digitalCodes[index];
      }
      return "";
    },

    showDialogbox() {
      if (this.validateForm()) {
        this.showDialog = true;
        this.requestotp(); // Show the dialog box if the form is valid
      }
    },

    validateForm() {
      if (
        this.firstname === "" ||
        this.lastname === "" ||
        this.email === "" ||
        this.dob === "" ||
        this.country === "" ||
        this.phone === "" ||
        this.referencecategory === "" ||
        this.language === "" ||
        this.comments === ""
      ) {
        alert("Please fill in all fields");
        return false;
      }
      return true;
    },

    async requestotp() {
      const formdata = {
        first_name: this.firstname,
        last_name: this.lastname,
        DOB: this.dob,
        email: this.email,
        country: this.country,
        phone: this.phone,
        reference: this.referencecategory,
        language: this.language,
        remark: this.comments,
      };

      try {
        
        const response = await axios.post(
          "http://89.47.164.122:4000/api/registrations/registerUser",
          {
            phone: this.phone,
            formdata,
          }
        );
        console.log(response.data);
        if (response.status === 200) {
          console.log("OTP sent successfully:", response.data);
          
          // this.$router.push('/demo');
        } 
      } catch (error) {
        console.error("Error requesting OTP:", error);
      }
    },

    async submitotp() {
  let OTP = this.otp;
  try {
    const response = await axios.post(
      "http://89.47.164.122:4000/api/registrations/verify_otp",
      {
        OTP: OTP,
        phone: this.phone,
      }
    );
    if (response.status === 200) {
      console.log(response, 'submit');
      alert("Registration Successful");
      // if (response.data.toLowerCase() === 'submit') {
        
      // }
      //  else {
      //   alert("Invalid OTP. Please try again.");
      // }
    }
  } catch (error) {
    console.error("Error while submitting OTP:", error);
    alert("An error occurred while verifying the OTP. Please try again.");
  }
}


    // async requestotp() {
    //   const formdata = {
    //     first_name: this.firstname,
    //     last_name: this.lastname,
    //     DOB: this.dob,

    //     email: this.email,
    //     country: this.country,
    //     phone: this.phone,
    //     reference: this.referencecategory,
    //     language: this.language,
    //     remark: this.comments,
    //   };
    //   try {
    //     console.log(formdata);
    //     const response = await axios.post(
    //       "http://89.47.164.122:4000/api/registrations/registerUser",
    //       {
    //         phone: this.phone,
    //         formdata,
    //       }
    //     );
    //     console.log(response.data);
    //     this.$router.push();

    //     console.log("OTP sent successfully:", data);
    //   } catch (error) {
    //     console.error("Error requesting OTP:");
    //   }
    // },

    // async Resendotp() {
    //       try {

    //         const response = await resendOTP(phoneNumber);
    //         console.log('OTP Resent:', response.data);

    //       } catch (error) {
    //         console.error('Error while resending OTP:', error);

    //       }
    //   },

    //     async  submitotp() {
    //       let OTP = this.otp;

    // try{
    //   const response = await axios.post("http://89.47.164.122:4000/api/registrations/verify_otp",
    // { data: OTP, phone : this.phone});

    //    if(OTP==this.otp)
    //    {
    //     alert('Registration Sucessful');
    //    }
    // }
    // catch (error) {
    //     console.error('Error while resending OTP:', error);
    //     // Handle error here
    //   }
    // }
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;500&display=swap');
* {
  margin: 0;
  font-family: "Poppins", sans-serif;
  max-width: 100vw;
}
.img {
  background-image: url("../components/step.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}
.img .lang {
  width: 16vw;
  height: 9vh;
  bottom: 35vh;
  border-radius: 5px;
  border: none;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.2);
  outline: none;
}
.play-btn-home {
  width: 3.5vw;
  height: 3.5vw;
  background-repeat: no-repeat;
  background-size: 80% 80%;
  bottom: 35vh;

  border-radius: 6px;
  border: none;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 0 0 10px;
}
.signup-button {
  position: absolute;
  right: 15vw;
  bottom: 10vw;
  background-color: #4d4f50;
  color: #fff;
  padding: 15px 30px;
  font-size: 18px;
  border-color: white;
  border-radius: 5px;
  cursor: pointer;
}
.lang {
  position: absolute;
  right: 15vw;
  bottom: 10vw;
  background-color: #4d4f50;
  color: #fff;
  padding: 15px 30px;
  font-size: 18px;
  border-color: white;
  border-radius: 5px;
  cursor: pointer;
}
.login-container {
  position: absolute;
  right: 0;
  top: 0;
  height: 100%;
  width: 70%;
  background-color: rgb(255, 255, 255);
  transition: transform 1s;
  transform: translateX(100%);
  display: flex;
  justify-content: center;
}
.image-background {
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 30%;
  background-image: url("../components/side.jpeg");
  background-size: cover;
  transform: translateX(0); /* Initially positioned on the left */
  transition: opacity 3s; /* Add a transition for opacity */
  stop-opacity: 0; /* Start with opacity set to 0 */
}
.show-login {
  transform: translateX(0);
}
.reg-hero {
  width: 100vw;
  height: 100vh;
  display: flex;
}
.play-btn img {
  width: 1vw;
}
.play-btn {
  width: 2.5vw;
  height: 2.5vw;
  background-repeat: no-repeat;
  background-size: 60% 60%;
  border-radius: 6px;
  border: none;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0 0 0 10px;
}
.hero-right {
  width: 100vw;
  height: 100vh;
  display: flex;
  top: 20vh;
  justify-content: center;
  background-image: url("../components/background.jpeg");

  background-size: cover;
  background-repeat: no-repeat;
  /* background-position: center; */
  background-position: 35% 16%;
  overflow: hidden;
  opacity: 0.9;
}
.reg-hero .hero-right-heading {
  display: flex;
  justify-content: center;
  margin: 5vh 0 5vh 0;
  font-size: 19px;
  color: #05616D;

}
.reg-hero .hero-right-content {
  height: 100vh;
  width: 55vw;
  position: relative;
  top: 7vh;
}

.hero-right-input-grp .input-grp .label {
  width: 16vw;
  height: 6vh;
  color: #05616D;
  font-weight:500;
  border-radius: 5px;
  border: none;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.2);
  outline: none;
}
.hero-right-input-grp .input-grp {
  display: flex;
  justify-content: space-around;
}
.hero-right-input-grp .remarks {
  width: 92%;
  height: 6vh;
  color: #05616D;
  border: none;
  outline: none;
  border-radius: 5px;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.2);
}
.hero-right-input-grp .submit button {
  width: 94%;
  height: 7vh;
  border: none;
  background-color: rgba(0, 0, 0, 0.7);
  border: none;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.7);
  color: white;
  border-radius: 5px;
  position: relative;
  left: 1.5vw;
}
.country-dropdown {
  position: relative;
  left: 1.5vw;
  width: 4vw;
  height: 6vh;
  border-radius: 5px;
  border: none;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5px;
}
.country-grp {
  display: flex;
  position: relative;
  top: -5vw;
}
.phone {
  width: 11vw;
  border: none;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
}
.gender {
  height: 7vh;
}
.hero-right-content {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
.hero-right-input-grp {
  width: 55vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
}
.ref-grp {
  width: 17vw;
  background-color: #fff;
  display: flex;
  justify-content: space-around;
  align-items: center;
  border: 0.5px solid rgba(0, 0, 0, 0.3);
  border-radius: 5px;
  box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.2);
}
.ref-grp .ref-sub-grp {
  display: flex;
  flex-direction: column;
}
/* footer ribbon */
.dob-grp {
  display: flex;
  position: relative;
  top: -2vw;
}
.dob-grp .dob {
  width: 12vw !important;
  position: relative;
  left: 1.5vw;
  color: #05616D;
}
.bottom-grp {
  height: 12vw !important;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  position: relative;
  top: -6.5vw;
}
.hero-right-radio-btn-grp {
  display: flex;
  justify-content: space-around;
  position: relative;
  top: -1vw;
}
.hero-right-content .hero-right-ribbon {
  color: rgb(22, 8, 8);
  display: flex;
  justify-content: space-between;
  position: relative;
  top: -17vh;
}
.hero-right-content .hero-right-ribbon .ribbon-grp {
  display: flex;
  
  flex-direction: column;
  align-items: center;
  /* margin:5vh 0 0 0; */
}

.modal {
  display: block;
  position: fixed;
  z-index: 1050;
  left: 0;
  top: 0;
  width: 50%;
  height: 50%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-dialog {
  position: relative;
  width: auto;
  height: auto;
  margin: 0.5rem;
  pointer-events: none;
}

.modal-content {
  position: relative;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  pointer-events: auto;
  background-color: #fefefe;
  background-clip: padding-box;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 0.3rem;
  outline: 0;
}

.modal-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  padding: 1rem;
  border-bottom: 1px solid #dee2e6;
  border-top-left-radius: 0.3rem;
  border-top-right-radius: 0.3rem;
}

.modal-title {
  margin-bottom: 0;
  line-height: 1.5;
  width: auto;
  display: flex;
  justify-content: center;
  position: relative;
}

.modal-body {
  position: relative;
  flex: 1 1 auto;
  padding: 1rem;
}

.modal-footer {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding: 0.75rem;
  border-top: 1px solid #dee2e6;
  border-bottom-right-radius: 0.3rem;
  border-bottom-left-radius: 0.3rem;
}
.btn-secondary {
  width: 80px;
}
</style>
