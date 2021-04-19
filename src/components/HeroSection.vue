<template>
<section class="relative">
  <div class="hero-image h-screen hero-image bg-cover text-center">
    <div class="p-3 bg-black h-screen relative w-full z-10 bg-opacity-60 min-w-screen">
      <div class="h-full">
        <h3 class="align-middle font-bold text-3xl m-auto text-green-400">The Hideaway Koh Lipe</h3>
        <div class="w-1/2 mx-auto mt-20">
          <p class="text-green-400">When are you visiting?</p>
          <div class="flex">
            <div class="m-5">
              <p class="text-red-400 leading-3" v-if="noCheckInDate">Please enter check in date.</p>
              <litepie-datepicker
                class="text-black m-5"
                ref="myRef"
                placeholder="Check In"
                as-single
                :formatter="formatter"
                v-model="checkInDate"
                @input="verifyCheckInDate()"
              />
            </div>
            <div class="m-5">
              <p class="text-red-400 leading-3" v-if="noCheckOutDate">Please enter check out date.</p>
              <litepie-datepicker
                class="text-black m-5"
                ref="myRef"
                placeholder="Check Out"
                as-single
                :formatter="formatter"
                v-model="checkOutDate"
              />
            </div>
          </div>
          <p v-if="noNumberOfGuests" class="text-red-400 leading-3">Please enter number of guests.</p>
          <label class="block m-5 flex">
            <div class="m-auto flex">
              <span class="text-white">Number of guests:</span>
              <select class="flex text-black form-select mt-1 block appearance-none rounded m-5" v-model="noOfPpl">
                <option v-for="index in 31" :key="index" v-text="index - 1"></option>
              </select>
            </div>
          </label>
          <button @click="goToBooking" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">Check availability</button>
        </div>
      </div>
    </div>
  </div>
</section>
</template>
<script>
import { ref } from 'vue';
import LitepieDatepicker from 'litepie-datepicker';

export default {
  components: {
    LitepieDatepicker
  },
  data () {
    return {
      checkInDate: '',
      checkOutDate: '',
      noOfPpl: 0,
      noCheckInDate: false,
      noCheckOutDate: false,
      noNumberOfGuests: false

    }
  },
  methods: {
    goToBooking () {
      if (!this.checkInDate) {
        this.noCheckInDate = true
      } else {
        this.noCheckInDate = false
      }

      if (!this.checkOutDate) {
        this.noCheckOutDate = true
      } else {
        this.noCheckOutDate = false
      }

      if (this.noOfPpl == 0) {
        this.noNumberOfGuests = true
      } else {
        this.noNumberOfGuests = false
      }

      if (!this.noCheckInDate && !this.noCheckOutDate && !this.noNumberOfGuests) {
        window.open(`https://www.booking.com/hotel/th/the-hideaway-koh-lipe.en-gb.html?checkin=${this.checkInDate};checkout=${this.checkOutDate};dest_id=900041042;group_adults=${this.noOfPpl}`, '_blank')
      }
    },
    verifyCheckInDate () {
      console.log(this.checkInDate)
      if (this.checkInDate < new Date()) {
        this.checkInDate = ''
      }
    }
  },
  setup() {
    const myRef = ref(null);
    const dateValue = ref([]);
    const formatter = ref({
      date: 'YYYY-MM-DD',
      month: 'MM'
    });

    return {
      myRef,
      dateValue,
      formatter
    };
  }
};
</script>
<style>
  .hero-image {
    background-image: url(../assets/hideawayhero.jpg)
  }
</style>
