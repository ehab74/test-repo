<template>
  <nav-bar></nav-bar>
  <the-loader v-if="showLoading"></the-loader>
  <base-card>
    <div class="alert alert-danger" v-if="error">{{ error }}</div>
    <!-- <div class="alert alert-success" v-if="isSuccess && error === '' ">You Signed up successfully</div> -->
    <form @submit.prevent="submitPatient">
      <label class="doctor">Sign Up as a patient !</label>
      <div class="form-row">
        <div class="col">
          <label>First Name</label>
          <input
            type="text"
            class="form-control"
            placeholder="First name"
            v-model="first_name"
            required
          />
        </div>
        <div class="col">
          <label>Last Name</label>
          <input
            type="text"
            class="form-control"
            placeholder="Last name"
            v-model="last_name"
            required
          />
        </div>
      </div>
      <div class="form-row">
        <div class="form-group col-md-6">
          <label for="inputEmail4">Email</label>
          <input
            type="email"
            class="form-control"
            id="inputEmail4"
            placeholder="xxx@email.com"
            v-model="email"
            required
          />
          <div class="error" v-if="errors.email">{{ errors.email }}</div>
        </div>
        <div class="form-group col-md-6">
          <label for="inputPassword4">Password</label>
          <input
            type="password"
            class="form-control"
            id="inputPassword4"
            v-model="password"
            required
          />
          <div class="error" v-if="errors.password">{{ errors.password }}</div>
        </div>
      </div>
      <div class="form-group">
        <label for="inputAddress2">User Name</label>
        <input
          type="text"
          class="form-control"
          id="inputmobile"
          v-model="username"
          required
        />
      </div>
      <div class="form-group">
        <label for="inputAddress2">Mobile Number</label>
        <input
          type="text"
          class="form-control"
          id="inputmobile"
          placeholder="+20 01.."
          v-model="mobile"
          required
        />
      </div>
      <div class="form-group">
        <label for="inputAddress">Address</label>
        <input
          type="text"
          class="form-control"
          id="inputAddress"
          placeholder="1234 Main St"
          v-model="address"
          required
        />
      </div>
           <div class="form-check">
  <input class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios1" value="1"  v-model="gender">
  <label class="form-check-label" for="exampleRadios1">
    Female
  </label>
</div>
<div class="form-check">
  <input class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios2" value="0" v-model="gender">
  <label class="form-check-label" for="exampleRadios2">
    Male
  </label>
</div>
        <div class="form-group">
          <label for="inputDate">Birth Date</label>
          <input
            type="date"
            class="form-control"
            id="inputDate"
            v-model="birthdate"
            required
          />
        </div>
      <button type="submit" class="btn btn-primary">Sign Up</button>
    </form>
  </base-card>
</template>
<script>
// import axios from 'axios';
import SignupValidations from '../../services/SignupValidations';
import { mapActions } from 'vuex';
import { mapState } from 'vuex';
import { SIGNUP_ACTION } from '../../store/storeconstants';
import TheLoader from '../ui/TheLoader.vue';

export default {
  components: { TheLoader },
  computed: {
    ...mapState({
      showLoading: state => state.showLoading
    })
  },
  data() {
    return {
      first_name: '',
      last_name: '',
      email: '',
      password: '',
      mobile: '',
      address: '',
      birthdate: '',
      gender: '',
      username: '',
      isSuccess: '',
      errors: [],
      error: ''
    };
  },
  methods: {
    ...mapActions('auth', {
      signup: SIGNUP_ACTION
    }),
    submitPatient() {
      let validtations = new SignupValidations(this.email, this.password);
      this.errors = validtations.checkValidations();
      if ('email' in this.errors || 'password' in this.errors) {
        return false;
      }
      this.signup({
        url: 'http://localhost:5000/patient/register',
        body: {
          email: this.email,
          password: this.password,
          first_name: this.first_name,
          last_name: this.last_name,
          birthdate: this.birthdate,
          username: this.username,
          gender: this.gender,
          mobile: this.mobile,
          address: this.address
        }
      })
        .then(() => {
          this.$router.push('/loginpatient');
        })
        .catch(error => {
          this.error = error;
        });

      //     axios
      // .post(
      //     `http://localhost:5000/patient/reg`,
      //     {first_name: this.first_name, last_name: this.last_name, email: this.email, password: this.password,
      //     mobile: this.mobile, address: this.address, age: this.age, gender: this.gender, username: this.username},
      //     )
      // .then((response) => {
      //     console.log(response);
      // });

      this.isSuccess = true;
    }
  }
};
</script>
<style scoped>
.doctor {
  text-align: center;
  font-size: 30px;
  margin-left: 170px;
}
</style>