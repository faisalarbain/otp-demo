<template>
  <section class="section">
    <div class="columns is-center">
      <div class="column has-text-centered">
        <b-button @click="openOtp" type="is-primary">OPEN OTP</b-button>
      </div>
    </div>
  </section>
</template>

<script>
import OTP from '@/components/OTP.vue';

export default {
  name: 'IndexPage',
  components: {
    
  },
  methods:{
    openOtp(){
      this.$buefy.modal.open({
        component: OTP,
        hasModalCard: true,
        canCancel: false
      })
    }
  }
}
</script>
