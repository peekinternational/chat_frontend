<template>
  <div class="hello">
    <div class="login-page1">
      <div class="container-fluid p-0">
        <div class="row">
          <div class="col-12">
            <div class="login-contain-main">
              <div class="left-page">
                <div class="login-content">
                  <div class="login-content-header"><img class="image-fluid" src="../assets/images/logo/logo_big.png" style="height:70px" alt="images"></div>
                  <h3 style="margin: 2px;">{{ $t("welcomeals") }}</h3>
                  <h4>{{ $t("welcomeals3") }}</h4>
                  <form v-on:submit="registeruser" class="form1">
                    <div class="form-group">
                      
                      <input
                        class="form-control"
                        id="inputname"
                        v-model="input.username"
                        type="text"
                        :placeholder="$t('Name')"
                        maxlength="20"
                        minlength="4"
                        required
                      />
                    </div>

                     <div class="form-group">
                      
                      <p v-if="userStatus" id="useridCheck" style="position: absolute; right:0px; padding-top: 13px;padding-right: 60px;"></p>
                      <input
                        class="form-control"
                        id="inputuserid"
                        v-model="input.userId"
                        type="text"
                        v-on:keyup="checkUserId"
                        :placeholder="$t('UserId')"
                        maxlength="15"
                        minlength="4"
                        required
                      />
                    </div>
                    <div class="form-group">
                     
                      <p v-if="emailStatus" id="emailCheck" style="position: absolute;right:0px;    padding-top: 13px;padding-right: 60px;"></p>
                      <input
                        class="form-control"
                        id="inputemail"
                        type="email"
                        v-model="input.email"
                        v-on:keyup="checkemail"
                        :placeholder="$t('emailorno')"
                        required
                      />
                    </div>
                    <div class="row">
                    <div class="form-group col-4">
                      <input type="number" class="form-control dob" v-model="input.dd" placeholder="" maxlength="31" name="" required> 
                    </div>
                    <div class="form-group col-4">
                        <input type="number" class="form-control dob" v-model="input.mm" placeholder="" maxlength="12" name="" required>
                    </div>
                    <div class="form-group col-4">
                        <input type="number" class="form-control dob" v-model="input.yyyy" placeholder="" name="" required>
                    </div>
                    </div>

                    <div class="form-group">
                      <input
                        class="form-control"
                        id="inputpassword"
                        v-model="password"
                        type="password"
                         maxlength="10"
                        minlength="4"
                        :placeholder="$t('Password')"
                        required
                      />
                    </div>
                      <div class="form-group">
                      
                      <p id="cpass" style="position: absolute; right: 0px; padding-top: 13px; padding-right: 60px;"></p>
                      <input
                        class="form-control"
                        id="inputconfirmpassword"
                        v-model="confirmpassword"
                        type="password"
                        :placeholder="$t('ConfirmPassword')"
                        required
                      />
                    </div>

                    <div class="form-group">
                      <div class="buttons">
                        <button
                          type="submit"
                          class="btn btn-primary button-effect" id="submitbtn" disabled
                        >
                          {{ $t('Signup') }}
                        </button>
                        <router-link
                          to="/login"
                          class="btn button-effect btn-signup"
                          >{{ $t('Login') }}</router-link
                        >
                      </div>
                    </div>
                  </form>

                  <div class="termscondition">
                    <h4 class="mb-0">
                      <span>*</span>{{ $t('Termsandcondition') }}<b>&amp;</b>Privacy
                      policy
                    </h4>
                  </div>
                </div>
              </div>
              <div class="right-page">
                <div class="right-login animat-rate">
                  <div class="animation-block">
                 <!--    <div class="bg_circle">
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                      <div></div>
                    </div> -->
                   <!--  <div class="cross"></div>
                    <div class="cross1"></div>
                    <div class="cross2"></div>
                    <div class="dot"></div>
                    <div class="dot1"></div>
                    <div class="maincircle"></div>
                    <div class="top-circle"></div>
                    <div class="center-circle"></div>
                    <div class="bottom-circle"></div>
                    <div class="bottom-circle1"></div>
                    <div class="right-circle"></div>
                    <div class="right-circle1"></div> -->
                    <img
                      class="heart-logo"
                      src="../assets/images/login_signup/5.png"
                      alt="login logo"
                    /><img
                      class="has-logo"
                      src="../assets/images/login_signup/4.png"
                      alt="login logo"
                    /><img
                      class="login-img"
                      src="../assets/images/login_signup/1s.png"
                      alt="login logo"
                    /><img
                      class="boy-logo"
                      src="../assets/images/login_signup/6.png"
                      alt="login boy logo"
                    /><img
                      class="girl-logo"
                      src="../assets/images/login_signup/7.png"
                      alt="girllogo"
                    /><!-- <img
                      class="cloud-logo"
                      src="../assets/images/login_signup/2.png"
                      alt="login logo"
                    /><img
                      class="cloud-logo1"
                      src="../assets/images/login_signup/2.png"
                      alt="login logo"
                    /><img
                      class="cloud-logo2"
                      src="../assets/images/login_signup/2.png"
                      alt="login logo"
                    /><img
                      class="cloud-logo3"
                      src="../assets/images/login_signup/2.png"
                      alt="login logo"
                    /><img
                      class="cloud-logo4"
                      src="../assets/images/login_signup/2.png"
                      alt="login logo"
                    /><img
                      class="has-logo1"
                      src="../assets/images/login_signup/4.png"
                      alt="login logo"
                    /> -->
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import $ from "jquery";
import JQuery from "jquery";
import "bootstrap";
import feather from "feather-icons";
import Popper from "popper.js";
import Datepicker from 'vuejs-datepicker';
import "feather-icons/dist/feather.min.js";
import tippy from "tippy.js";
import "tippy.js/dist/tippy.css";

import {
  AirplayIcon,
  AtSignIcon,
  PhoneIcon,
  VideoIcon,
  SmileIcon,
  MicIcon,
  SendIcon,
  MessageSquareIcon,
  UsersIcon,
  PlusCircleIcon,
  PlusIcon,
  PhoneIncomingIcon,
  PhoneOutgoingIcon,
  FileIcon,
  ClockIcon,
  ListIcon,
  GridIcon,
  BookIcon,
  XIcon,
  DownloadIcon,
  SearchIcon,
  StarIcon,
  MoreVerticalIcon,
} from "vue-feather-icons";
import carousel from "vue-owl-carousel";

export default {
  name: "Signup",
  components: {
    carousel,
    PhoneIncomingIcon,
    PhoneIcon,
    Datepicker,
    VideoIcon,
    SmileIcon,
    MicIcon,
    SendIcon,
    MessageSquareIcon,
    UsersIcon,
    PlusCircleIcon,
    PlusIcon,
    PhoneOutgoingIcon,
    FileIcon,
    ClockIcon,
    ListIcon,
    GridIcon,
    BookIcon,
    XIcon,
    DownloadIcon,
    SearchIcon,
    StarIcon,
    MoreVerticalIcon,
  },
  props: [],
  data() {
    return {
      input: {
        username: "",
        email: "",
        dd: "",
        mm: "",
        yyyy: "",
        userId:"",
      },
      password: "",
      confirmpassword:'',
      userStatus:false,
      emailStatus:false,
    };
  },
  watch: {
    confirmpassword(){
      if(this.confirmpassword == this.password){
         $('#cpass').css('color','green');
         $('#cpass').text('Password Match');
        $('#submitbtn').prop('disabled', false);

      }else{
        $('#cpass').css('color','red');
        $('#cpass').text('Password Not Match');
        $('#submitbtn').prop('disabled', true);
      }
    },
    password(){
      if(this.confirmpassword){
         if(this.confirmpassword == this.password){
         $('#cpass').css('color','green');
         $('#cpass').text('Password Match');
        $('#submitbtn').prop('disabled', false);

      }else{
        $('#cpass').css('color','red');
        $('#cpass').text('Password Not Match');
        $('#submitbtn').prop('disabled', true);
      }
      }
      
    }
  },
  methods: {
    checkUserId() {
      if(this.input.userId.length > 3){
  axios.post("/projects/checkuserid", {
          projectId: "5d4c07fb030f5d0600bf5c03",
          userId: this.input.userId,
        })
        .then(
          (response) => {
            console.log(response);
            if(response.data.status == true){
              this.userStatus=true;
              $('#useridCheck').css('color','red');
                $('#useridCheck').text('Not Avaliable');

            }else{
              this.userStatus=true;
              $('#useridCheck').css('color','green');
               $('#useridCheck').text('Avaliable!');
            }
         
          },
          function (err) {
            console.log("err", err);
            alert(err.body);
          })
      }else{
        this.userStatus=false;
      }
    },

        checkemail() {
          var str1=this.input.email;
          if(str1.indexOf('@') != -1){
      axios.post("/projects/checkemail", {
          projectId: "5d4c07fb030f5d0600bf5c03",
          email: this.input.email,
        })
        .then(
          (response) => {
            console.log(response);
            if(response.data.status == true){
              this.emailStatus=true;
              $('#emailCheck').css('color','red');
                $('#emailCheck').text('Email Already Exist');

            }else{
              this.emailStatus=true;
              $('#emailCheck').css('color','green');
               $('#emailCheck').text('Avaliable!');
            }
         
          },
          function (err) {
            console.log("err", err);
            alert(err.body);
          })
      }else{
        this.emailStatus=false;
      
}
    },
    registeruser: function (event) {
      event.preventDefault();

      axios
        .post("/projects/register-user", {
          projectId: "5d4c07fb030f5d0600bf5c03",
          name: this.input.username,
          userId: this.input.userId,
          email: this.input.email,
          birth: this.input.yyyy+'-'+this.input.mm+'-'+this.input.dd,
          password: this.password,
        })
        .then(
          (response) => {
            console.log(response);
            if (response.data != "") {
               if(response.data.status == 0){
               this.$toasted.error("User name or email already exist !!", {
                theme: "toasted-primary",
                position: "top-left",
                duration: 5000,
              });
              }else if(response.data.status == 1){
               this.$toasted.success("Register Successfully Please check your email and verify your account !!", {
                theme: "toasted-primary",
                position: "top-left",
                duration: 5000,
              });
              //this.$router.push("/login");
              }else{
                 this.$toasted.error("Error !!", {
                theme: "toasted-primary",
                position: "top-left",
                duration: 5000,
              });
              }
            } else {
              this.$toasted.error("Error !!", {
                theme: "toasted-primary",
                position: "top-left",
                duration: 5000,
              });
            }
          },
          function (err) {
            console.log("err", err);
            alert(err.body);
          }
        );
    },
  },
  mounted() {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >

.dob input {
      border: none !important;
    background: transparent !important;
    width: 100%;
}
.login-content .form1 .form-group, .login-content .form2 .form-group {
    margin-bottom: 15px;
}
</style>
