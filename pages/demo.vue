<template>
  <div>
    <button @click="showDialog = true" class="btn btn-primary">Open Dialog</button>

    <!-- Dialog Box -->
    <div class="modal" tabindex="-1" role="dialog" style="display: block" v-if="showDialog">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">OTP Dialog Box</h5>
            <button type="button" class="close" @click="showDialog = false">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <div v-if="isOTPOpen">
              <input v-model="otp" type="text" placeholder="Enter OTP" />
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" @click="showDialog = false">Close</button>
            <!-- Add your submit functionality here -->
            <button type="button" class="btn btn-primary" @click="submitForm">Submit</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showDialog: false,
      isOTPOpen: true, // Modify this based on your conditions
      otp: '',
    };
  },
  methods: {
    submitForm() {
      // Handle submit logic here
      // For example, you can print the OTP to the console
      console.log('Submitted OTP:', this.otp);
      // You can add more complex logic for submitting the form here
      // Close the dialog box after submitting
      this.showDialog = false;
    },
  },
};
</script>
