<template>
  <div class="hello">
    <div class="page">
      <div class="page-cover">
        <div class="page-logo">
          <img src="../assets/images/logo.svg" />
        </div>
        <div class="cover-img">
          <img src="../assets/images/cover-img.svg" />
        </div>
        <ul class="cover-list">
          <li class="cover-list-item global-icon">
            Powerful and reliable global network
          </li>
          <li class="cover-list-item cloud-icon">
            Modern & Agile CDN infrastructure
          </li>
          <li class="cover-list-item head-icon">15 years of CDN experience</li>
          <li class="cover-list-item design-icon">
            Direct access to engineers with Slack
          </li>
        </ul>
      </div>
      <div class="page-form">
        <h1 class="form-title">Start a 14-day instant <b>free trial</b></h1>
        <div class="form-description">
          Give your website the <b>speed it deserves</b>. With the fastest,
          next-generation CDN.
        </div>

        <form class="form-list" id="form" method="post">
          <input
            type="text"
            name="name"
            class="form-item"
            placeholder="First Name *"
          />
          <input
            type="text"
            name="surname"
            class="form-item"
            placeholder="Last Name *"
          />
          <input
            type="text"
            name="company"
            class="form-item"
            placeholder="Company"
          />
          <input
            type="email"
            name="email"
            class="form-item"
            placeholder="Business E-mail*"
          />
          <input
            type="text"
            name="phone"
            class="form-item"
            placeholder="Phone"
          />
          <input
            type="password"
            name="password"
            class="form-item"
            placeholder="Password *"
          />
          <input
            type="password"
            name="repassword"
            class="form-item"
            placeholder="Re-enter Password *"
          />

          <button
            class="form-submit-btn"
            type="submit"
            @click="submitted = true"
            :disabled="submitted"
            @click.prevent="loginForm()"
          >
            START TRIAL
          </button>
        </form>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
import Swal from "sweetalert2/dist/sweetalert2.js";
export default {
  name: "HelloWorld",
  props: {},
  data() {
    return {
      submitted: false,
    };
  },
  methods: {
    loginForm: function () {
      let form = document.getElementById("form");
      let formData = new FormData(form);

      let name = formData.get("name");
      let surname = formData.get("surname");
      let company = formData.get("company");
      let email = formData.get("email");
      let phone = formData.get("phone");
      let password = formData.get("password");
      let repassword = formData.get("repassword");
      //console.log(name + " - " + surname);

      if (password.length > 0 && password === repassword) {
        const api = "https://jsonplaceholder.typicode.com/users";

        axios
          .post(api, {
            name: name,
            surname: surname,
            company: company,
            email: email,
            phone: phone,
            password: password,
          })
          .then((response) => {
            console.log(response.data);
            //console.log(response.status);

            if (response.status === 201) {
              Swal.fire({
                title: "Success!",
                text: "Registration successful!",
                icon: "success",
                confirmButtonText: "Ok",
              });
              this.submitted = false;
              form.reset();
            }
          })
          .catch(function (error) {
            console.log(error);

            Swal.fire({
              title: "Error!",
              text: "Something went wrong!",
              icon: "error",
              confirmButtonText: "Ok",
            });
            this.submitted = false;
          });
      } else {
        Swal.fire({
          title: "Error!",
          text: "Password error. Check your password!",
          icon: "error",
          confirmButtonText: "Ok",
        });
        this.submitted = false;
      }
    },
  },
};
</script>

