<template>
  <div class="container">
    <div id="app">
      <div><h2>Form Screen</h2><hr></div>
      <b-form @submit="onSubmit" @reset="onReset" v-if="show">
        <b-form-group
          id="input-group-1"
          label="Email address:"
          label-for="input-1"
          description="We'll never share your email with anyone else."
        >
          <b-form-input
            id="input-1"
            v-model="form.email"
            type="email"
            required
            placeholder="Enter email"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="form.name"
            required
            placeholder="Enter name"
          ></b-form-input>
        </b-form-group>

        <div>
          <label for="example-datepicker">Choose a date</label>
          <b-form-datepicker
            id="example-datepicker"
            v-model="form.date"
            class="mb-2"
          ></b-form-datepicker>
        </div>

        <b-form-group id="input-group-4" label="Country:" label-for="input-4">
          <b-form-select
            id="input-4"
            v-model="form.country"
            :options="countries"
            required
          ></b-form-select>
        </b-form-group>

        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
      </b-form>
    </div>
    <div>
      <b-table striped hover :items="newForm" :fields="fields"></b-table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fields: ["email", "name", "date","country"],

      form: {
        email: "",
        name: "",
        date: "",
        country: null
      },
      newForm: [],
      countries: [
        { text: "Select Country", value: null },
        "Turkey",
        "Germany",
        "U.S.A",
        "Spain",
        "Portugal"
      ],
      show: true
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      this.newForm.push(this.form);
      console.log(this.newForm);
    },

    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.email = "";
      this.form.name = "";
      this.form.date = "";
      this.form.country = null;
      // Trick to reset/clear native browser form validation state
      this.$nextTick(() => {
        this.show = true;
      });
    }
  }
};
</script>
<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>