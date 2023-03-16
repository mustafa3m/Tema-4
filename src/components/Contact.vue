<template>
  <section class="contact">
    <form @submit="submitForm" class="contact__form" action="#">
      <h2 class="underline"><strong>Newsletter sign-up</strong></h2>

      <label for="name">Name</label>
      <input v-model="form.name" type="text" />
      <label for="age">Age</label>
      <input v-model="form.age" type="number" />
      <label for="email">Email</label>
      <input v-model="form.email" type="email" />
      <label for="password">Password</label>
      <input v-model="form.password" :type="passwordFieldType" placeholder="Password"/>
      <label for="adress">Adress</label>
      <input v-model="form.adress" type="text" />
      <label for="adress">Country</label>
      <input v-model="form.country" type="text" />

      <div>
        <button @click="switchVisibility" type="submit" class="btn btn-dark bottom"> Submit </button>
      </div>
      <ul v-if="errors.length">
        <!-- iterate over error -->
        <li class="error-red" v-for="error in errors" :key="error">
          {{ error }}
        </li>
      </ul>
    </form>

    <!-- display of resultat  for the Newsletter -->
    <div class="display__resultat">
      <p>Name: {{ form.name }}</p>
      <p>Age: {{ form.age }}</p>
      <p>Email: {{ form.email }}</p>
      <p class="display__resultat__password">Password: {{ form.password }}</p>
      <p>Adress: {{ form.adress }}</p>
      <p>Country: {{ form.country }}</p>
    </div>
  </section>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          name: "",
          password: "",
          email: "",
          adress: "",
          age: "",
          country: "",
        },

        errors: [],
      };
    },
    methods: {
      /* hide password */
      switchVisibility() {
        this.passwordFieldType =
          this.passwordFieldType === "password" ? "text" : "password";
      },
      /* Form modifier and submit */
      submitForm(event) {
        event.preventDefault();

        if (this.verifyForm()) {
          console.log({ ...this.form });
        } else {
          console.log("error ");
        }
      },
      /* Validation of forms */
      verifyForm() {
        this.errors = [];
        if (!this.form.password) {
          this.errors.push("password missing");
        }
        if (this.form.password && this.form.password.length < 6) {
          this.errors.push("password should be at least 6 characters");
        }

        return this.errors.length ? false : true;
      },
    },
  };
</script>

<style scoped>
  /* contact */

  .contact {
    padding: 10rem 1rem;
    display: flex;
    justify-content: space-between;
    gap: 5rem;
  }

  .contact__form {
    max-width: 600px;
    display: flex;
    flex-direction: column;
    width: 100%;
  }
  .contact__form input {
    background: #333;
    border: 0;
    border-bottom: 1px solid #555;
    padding: 1rem;
    font-size: 1.3rem;
    color: white;
    outline: 0;
    
  }
  .contact__form button {
    display: block;
    margin: 3rem auto;
    padding: 1rem 2rem;
    border: 0;
    border-radius: 30px;
    background: #f1c40f;
    color: white;
    font-weight: 700;
    font-size: 1.3rem;
    cursor: pointer;
  }

  .display__resultat {
    width: 100%;
    margin-top: 200px;
    padding: 1rem 2rem;
  }

  .error__red {
    color: red;
  }
  .display__resultat__password {
    display: none;
  }
  .underline{
    margin-bottom: 2rem;
    font-size:3rem;

  }
  .contact__form h2 strong{
    font-size:3rem;
    margin-bottom: 2rem;
    
  }


  @media only screen and (max-width: 600px) {
    .underline{
    margin-bottom: 1rem;
    font-size:1.5rem;

  }

  }
</style>
