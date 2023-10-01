<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset">
      <b-form-group id="input-group-2" label="Subject" label-for="input-2">
        <b-form-input
            id="input-2"
            v-model="form.topic"
            placeholder="e.g. support answer"
            required
        ></b-form-input>
      </b-form-group>

      <b-form-group
          id="input-group-1"
          label="Type your message"
          label-for="textarea"
          description="User will be notified about your message"
      >
        <b-form-textarea
            id="textarea"
            v-model="form.message"
            placeholder="Dear emploee, ..."
            rows="3"
            max-rows="6"
        ></b-form-textarea>
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
        topic: '',
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