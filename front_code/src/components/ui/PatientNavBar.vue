<template>
<div class="navigation">
  <nav class="navbar navbar-expand flex-column flex-md-row bg-light">
    <div class="container-fluid">
      <router-link to="doctorhome" class="navbar-brand" id="box"
        >Welcome</router-link
      >
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavDropdown"
        aria-controls="navbarNavDropdown"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavDropdown">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link
              to="/patienthome"
              class="nav-link active"
              aria-current="page"
              >Home</router-link
            >
          </li>
          <li class="nav-item">
            <router-link to="/patientaboutus" class="nav-link">About Us</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/patientdoctors" class="nav-link">Doctors</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/patientcontactus" class="nav-link"
              >Contact Us</router-link
            >
          </li>
          <div class="dropdown">
            <button
              class="btn btn-secondary dropdown-toggle"
              type="button"
              id="dropdownMenuButton"
              data-toggle="dropdown"
              aria-haspopup="true"
              aria-expanded="false"
              style="background-color: transparent; color: #0069D9; padding: 0;border: none;background: none;"
            >
              My Actions
            </button>
            <div class="dropdown-menu" aria-labelledby="dropdownMenuButton">
              <router-link to="/bookappointment" class="dropdown-item"
                >Book Appointment</router-link
              >
              <router-link to="/viewappointment" class="dropdown-item"
                >My Appointments</router-link
              >
              <router-link to="/doctorprescription" class="dropdown-item"
                >Doctor's Examination</router-link
              >
            </div>
          </div>
          <div class="logout">
            <li class="nav-item">
              <a href="#" class="nav-link" @click.prevent="onLogout">Logout</a>
            </li>
          </div>
        </ul>
      </div>
    </div>
  </nav>
</div>
</template>
<script>
import axios from 'axios';
export default {
  methods: {
    onLogout() {
      axios.post(
        'http://localhost:5000/logout',
        {},
        {
          headers: {
            Authorization: 'Bearer ' + localStorage.getItem('token')
          }
        }
      );
      this.$router.replace('/loginpatient');
    }
  }
};
</script>
<style scoped>
.navigation {
  width: 100%;
}
.dropdown {
  padding: 5px;
}
.logout {
  padding: 5px;
}
#box {
  margin-bottom: 12px;
  font-weight: bold;
}
</style>
