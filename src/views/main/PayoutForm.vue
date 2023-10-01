<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset">
      <b-form-group
          id="input-group-1"
          label="Enter payout sum in RUB:"
          label-for="input-1"
          description="This sum will be requested to payout."
      >
        <b-form-input
            id="input-1"
            v-model="form.sumRUB"
            type="text"
            placeholder="1000.00"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Request message:" label-for="input-2">
        <b-form-input
            id="input-2"
            v-model="form.message"
            placeholder="Request message"
            required
        ></b-form-input>
      </b-form-group>

      <b-button class="mr-2" type="submit" variant="danger">Submit</b-button>
      <b-button type="reset" >Cancel</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        sumRUB: '',
        message: ''
      },
    }
  },
  methods: {
    onSubmit() {
      this.$emit('hide-details')
    },
    onReset() {
      this.$emit('hide-details')
    }
  }
}
</script>

<style scoped>

</style>