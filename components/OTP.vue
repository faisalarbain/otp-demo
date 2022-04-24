<template>
    <div style="padding:20px;" @click="focusInput">
      <div class="modal-card">
        <header class="modal-card-head">
            <p class="modal-card-title">OTP</p>
            <button type="button" class="delete" @click="$emit('close')" />
        </header>
        <section class="modal-card-body" :class="{'is-focus': isFocus}">
          <b-field>
            <b-checkbox v-model="show">Show Phantom input</b-checkbox>
          </b-field>
          <div class="columns is-mobile">
            <div v-for="(pin,i) in displayPin" class="column" style="padding:5px;" :key="i">
              <otp-pin :display="pin" :isHiglight="isHighlight(i)" />
            </div>
          </div>
          <div class="buttons">
            <b-button @click="submit" :disabled="!isValid" type="is-primary">Submit</b-button>
          </div>
            
          <div class="box phantom-otp" :class="{'is-sr-only': !show}" style="width:300px;">
            <input ref="otpInput" type="tel" v-model="otpInput" @focus="isFocus = true" @blur="isFocus = false">
            <div class="notification content help">
              <p>Note</p>
              <p>User input in single textfield. from the inputed value, we parse for the otp input</p>
              <p>This will enable paste support as well</p>
            </div>
          </div>
        </section>
      </div>
    </div>
</template>

<script>
import OtpPin from './OtpPin.vue';
export default {
  components:{
    OtpPin
  },
  data(){
    return {
      blurCounter: 0,
      otpInput: '',
      size: 6, 
      show: false,
      isFocus: false
    }
  },
  mounted(){
    this.$nextTick(() => {
      this.focusInput()
    })
  },
  watch:{
    otpInput(value){
      this.otpInput = value.replace(/[^0-9]/g, '').substring(0,this.size);
    }
  },
  computed:{
    displayPin(){
      const paddings = " ".repeat(this.size)
      return `${this.otpInput}${paddings}`.substring(0,this.size)
        .split("")
        .map((value) => value === " " ? "" : "•")
    },
    isValid(){
      return this.otpInput.length == this.size
    }
  },
  methods:{
    focusInput(){
      console.log("lost....")
      this.$nextTick(() => {
        this.$refs.otpInput.focus();
        console.log(this.$refs.otpInput, "focus back")
      })
    },
    isHighlight(idx){
      return idx == this.otpInput.length
    },
    submit(){
      alert(`OTP submit: ${this.otpInput}`)
    }
  }
  
}
</script>

<style >
.phantom-otp {
  position: fixed;
  bottom:0;
  right:0;
}
</style>