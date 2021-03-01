<template>
  <fieldset>
    <legend>Filter Available Hotels</legend>
    <div
      class="d-flex flex-column flex-md-row align-items-center justify-content-center border rounded p-3"
    >
      <section class="m-3 d-flex align-items-center">
        <label for="from-datepicker" class="mr-3 my-0">From</label>
        <b-form-datepicker
          id="from-datepicker"
          v-model="FilterDateFromObj.value"
          class=""
          :min="FilterDateFromObj.min"
          :max="FilterDateFromObj.max"
        ></b-form-datepicker>
      </section>
      <section class="m-3 d-flex align-items-center">
        <label for="to-datepicker" class="mr-3 my-0">To</label>
        <b-form-datepicker
          id="to-datepicker"
          v-model="FilterDateToObj.value"
          :min="FilterDateToObj.min"
          :max="FilterDateToObj.max"
          class=""
        ></b-form-datepicker>
      </section>
      <b-button class="m-3">Show Available Rooms</b-button>
    </div>
  </fieldset>
</template>

<script>
export default {
  data() {
    return {
      FilterDateFromObj: {
        value: "",
        min: "",
        max: "",
      },
      FilterDateToObj: {
        value: "",
        min: "",
        max: "",
      },
    };
  },
  watch: {
    FilterDateFromObj: {
      handler(obj) {
        this.FilterDateToObj.min = obj.value;
        console.log(obj.value);
      },
      deep: true,
    },
    FilterDateToObj: {
      handler(obj) {
        this.FilterDateFromObj.max = obj.value;
        console.log(obj.value);
      },
      deep: true,
    },
  },
};
</script>