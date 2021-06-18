<template>
  <div class="w-screen">
    <navbar></navbar>
    <div class="detail-booking px-10 py-5">
      <div class="title text-2xl">
        Detail Booking
      </div>
      <hr class="my-4">
      <div class="detail">
        <div class="pod-name">
          Pod Name : {{ booking.pod_name }}
        </div>
        <div class="user-name">
          User Name : {{ booking.user_name }}
        </div>
        <div class="phone">
          User Phone : {{ booking.phone }}
        </div>
        <div class="status">
          Book Status : {{ booking.status }}
        </div>
        <div class="date">
          Book Date : {{ booking.booking_date }}
        </div>
        <div class="time">
          Book time : {{ booking.booking_time }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import navbar from '../../components/Nav.vue';
import axios from 'axios';
export default {
  data() {
    return {
      booking: [],
      params: this.$route.params
    }
  },
  components: {
    navbar,
  },
  mounted() {
    this.getBookingDetail()
  },
  methods: {
    getBookingDetail(url = 'http://127.0.0.1:8000/api/v1/booking/'+this.params.booking) {
      axios.get(url)
      .then( response => {
        this.booking = response.data
      })
      .catch(error => {
        console.log(error)
      })
    }
  }
}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS
.container {
@apply min-h-screen flex justify-center items-center text-center mx-auto;
}
*/
</style>
