<template>
  <div class="box has-text-centered otpPin" :class="boxStyle" >
    <p class="title is-5">{{display || '&nbsp;'}}</p>
  </div>
</template>

<script>
export default {
  props:["display", "isHiglight"],
  computed:{
    boxStyle(){
      return {
        otpPinEntered: this.display,
        otpPinFocus: this.isHiglight
      }
    }
  }
}
</script>

<style>
.otpPin {
  border: solid 1px transparent;
}

.otpPinEntered {
  border-color: inherit;
}

.is-focus .otpPinFocus {
  border-color: blue !important;
}


</style>