<template>
  <div class="w-screen">
    <navbar></navbar>
    <div class="bookin-list p-20">
      <div class="header flex flex-col">
        <div class="title text-2xl">
          Booking List
        </div>
        <div class="filter flex my-4">
          <input v-model="pod_name" type="text" placeholder="search pod name" class="border p-1 mx-1">
          <select v-model="status" class="border p-1 text-black mx-1">
            <option value="">Pilih Status</option>
            <option>booked</option>
            <option>expired</option>
            <option>done</option>
          </select>
          <div class="book_date flex mx-1">
            <div class="from-date flex items-center">
              <label for="date-from" class="mx-2">From :</label>
              <input v-model="bookingdategte" type="date" class="border p-1">
            </div>
            <div class="to-date flex items-center">
              <label for="date-to" class="mx-2">To :</label>
              <input v-model="bookingdatelte" type="date" class="border p-1">
            </div>
          </div>
          <div class="filter text-white bg-green-500 p-2 rounded-md cursor-pointer mx-2">
            <button  @click.prevent="getBookingList()">Filter</button>
          </div>
        </div>
      </div>
      <div class="bookingList flex flex-wrap">
        <div class="bookingItem bg-green-400 my-2 px-5 py-2 w-2/2  rounded-md mx-2 cursor-pointer hover:shadow-lg" v-for="booking in bookingList.results" :key="booking.id">
          <div @click="$router.push({path:'/booking/'+booking.id})" class="card-body flex justify-start">
            <div class="card-left">
              <div class="card-first-level text-white flex justify-around">
                <div class="pod-name mx-2">
                  <div class="labe text-sm">
                    Pod Name
                  </div>
                  <div class="name text-3xl font-semibold">
                    {{ booking.pod_name }}
                  </div>
                </div>
                <div class="status mx-2">
                  <div class="label text-sm">
                    Status :
                  </div>
                  <div class="name text-3xl font-semibold">
                    {{ booking.status }}
                  </div>
                </div>
              </div>
              <div class="card-second-level text-white flex">
                <div class="pod-name mx-2">
                  <div class="labe text-xs">
                    User Name :
                  </div>
                  <div class="name text-lg font-semibold">
                    {{ booking.user_name }}
                  </div>
                </div>
                <div class="pod-name mx-2">
                  <div class="labe text-xs">
                    Phone :
                  </div>
                  <div class="name text-lg font-semibold">
                    {{ booking.phone }}
                  </div>
                </div>
                <div class="price mx-2">
                  <div class="label text-xs">
                    Price :
                  </div>
                  <div class="name text-lg font-semibold">
                    {{ booking.price }}
                  </div>
                </div>
              </div>
            </div>
            <div class="card-right">
              <div class="booking mx-2 text-white">
                  <div class="date">
                    <div class="label text-md">
                      Booking Date :
                    </div>
                    <div class="name text-2xl font-semibold">
                      {{ booking.booking_date }}
                    </div>
                  </div>
                  <div class="time">
                    <div class="label text-md">
                      Booking Time
                    </div>
                    <div class="name text-2xl font-semibold">
                      {{ booking.booking_time }}
                    </div>
                  </div>
                </div>
            </div>
          </div>
        </div>
      </div>
      <div class="link flex">
          <div class="previous w-20 text-white bg-green-500 p-2 rounded-md cursor-pointer" v-if="bookingList.previous">
            <div  @click="getBookingList(bookingList.previous)">Previous</div>
          </div>
          <div class="next w-20 text-white bg-green-500 p-2 rounded-md cursor-pointer" v-if="bookingList.next">
            <div @click="getBookingList(bookingList.next)">Next</div>
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
      bookingList: [],
      pod_name: null,
      price: null,
      bookingdatenow: null,
      bookingdatelte: null,
      bookingdategte: null,
      status: '',
    }
  },
  components: {
    navbar,
  },
  mounted() {
    this.getBookingList()
  },
  methods: {
    getBookingList(url = 'http://127.0.0.1:8000/api/v1/booking-list/') {
      axios.get(url,{
        params: {
          pod_name__icontains: this.pod_name,
          price: this.price,
          status: this.status,
          booking_date__iexact: this.bookingdatenow,
          booking_date__lte: this.bookingdatelte,
          booking_date__gte: this.bookingdategte
        }
      })
      .then( response => {
        this.bookingList = response.data
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
