<template>
  <div>

    <!-- button ::::::::::: -->
    <button
        v-if="constructor === 'button'"
        class="btn btn-button"
        :class="[size, color]"
    >
      <slot>{{ defaultContent }}</slot>
    </button>


    <!-- link ::::::::::: -->
    <a
        v-if="constructor === 'link'"
        class="btn btn-link"
        :class="[size, color]"
        href="#"
    >
      <slot>{{ defaultContent }}</slot>
    </a>


    <!-- basket ::::::::::: -->
    <a
        v-if="constructor === 'basket'"
        class="btn btn-link btn-basket"
        :class="[size, color]"
        href="#"
        @click.prevent=""
    >
      <span class="btn-basket__number">
        <slot name="number">
          {{ productNumber }}
        </slot>
      </span>
      <slot name="content">{{ defaultContent }}</slot>
    </a>


    <!-- btnPlusOne ::::::::::: -->
    <a
        v-if="constructor === 'btnPlusOne'"
        class="btn btn-link btn-plus-one"
        :class="[size, color, classPlusOne]"
        href="#"
        @click.prevent="btnPlusOne"
    >
      <span class="btn-plus-one__text">
        <slot name="content">{{ defaultContent }}</slot>
      </span>
      <span v-if="btnPlusOneCounter" class="btn-plus-one__number">
        +{{ btnPlusOneCounter }}
      </span>
    </a>


    <!-- btnCounter ::::::::::: -->
    <div v-if="constructor === 'btnCount'" :class="classBtnCounter">
      <a
          class="btn btn-link"
          :class="[size, color]"
          href="#"
          @click.prevent="btnCounterReplacer"
          v-if="!classBtnCounter"
      >
        <slot name="content">{{ defaultContent }}</slot>
      </a>
      <div v-if="classBtnCounter" class="btn-count__counter" :class="size">
        <div @click.prevent="counterMinus" class="btn-counter-minus">
          <svg
              fill="none"
              height="2"
              viewBox="0 0 18 2"
              width="18"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="m0 1c0-.552285.447715-1 1-1h16c.5523 0 1 .447715 1 1 0 .55228-.4477 1-1 1h-16c-.552284 0-1-.44772-1-1z"
                :fill="color"
            />
          </svg>
        </div>
        <div class="btn-counter-number">
          <input type="text" v-model="btnCountCounter" @keypress.="counterChange" maxlength="2" :style="'outline-color:'+color">
        </div>
        <div @click.prevent="counterPlus" class="btn-counter-plus">
          <svg
              fill="none"
              height="18"
              viewBox="0 0 18 18"
              width="18"
              xmlns="http://www.w3.org/2000/svg"
          >
            <path
                d="m8 17c0 .5522.44775 1 1 1s1-.4478 1-1v-7h7c.5522 0 1-.44775 1-1s-.4478-1-1-1h-7v-7c0-.552246-.44775-1-1-1s-1 .447754-1 1v7h-7c-.552246 0-1 .44775-1 1s.447754 1 1 1h7z"
                :fill="color"
            />
          </svg>
        </div>
      </div>
    </div>


  </div>
</template>

<script>
// import { onBeforeMount } from "vue";

export default {
  data() {
    return {
      defaultContent: "Button default",
      productNumber: 5,
      btnPlusOneCounter: 0,
      classPlusOne: "",
      btnCountCounter: 0,
      classBtnCounter: "",
    }
  },
  // setup() {
  //   onBeforeMount(() => {
  //     let btnP1 = document.querySelector(".btn-plus-one");
  //     if (btnP1) {
  //       // btnP1.style.width = btnP1.offsetWidth + 1 + "px";
  //       console.log(btnP1.offsetWidth);
  //     }
  //   });
  // },
  props: {
    constructor: {
      type: String,
      validator(value) {
        return [
          "link",
          "button",
          "basket",
          "btnPlusOne",
          "btnCount",
        ].includes(value)
      },
      default: "button",
      required: true,
    },
    size: {
      type: String,
      validator(value) {
        return ["small", "medium", "big"].includes(value)
      },
      default: "medium",
    },
    color: {
      type: String,
      validator(value) {
        return ["green", "red", "outline"].includes(value)
      },
      default: "green",
    },
    // disabled: {
    //   type: String,
    //   validator(value) {
    //     return ["", "disabled"].includes(value);
    //   },
    //   default: "",
    // },
  },
  methods: {
    btnPlusOne() {
      this.btnPlusOneCounter += 1
      this.classPlusOne = "plus-one-counter"
    },
    btnCounterReplacer() {
      this.btnCountCounter++
      this.classBtnCounter = "btn-count"
    },
    counterMinus() {
      this.btnCountCounter--
      this.counterChange()
    },
    counterPlus() {
      this.btnCountCounter++
    },
    counterChange(){
      if(this.btnCountCounter === 0){
        this.classBtnCounter = ""
      }
    },
  },
};
</script>

<style lang="sass" scoped>
$color-dark: #2c3e50
$color-yellow: #FFCD5D
$border-radius: 6px
@mixin btn-flex()
  display: inline-flex
  align-items: center
  justify-content: center

.btn, .btn *
  box-sizing: border-box
.btn
  cursor: pointer
  border-radius: $border-radius
  color: #ffffff
  font-weight: 600
  @include btn-flex

.btn-button
  border: none
.btn-link
  text-decoration: none
.outline
  background-color: transparent

// Colors :::::::::::
.green
  background-color: #3FB983
.red
  background-color: #FF5C6A
.outline
  border: 1px solid $color-dark
  color: $color-dark

// Size :::::::::::
.big
  font-size: 18px
  height: 56px
  padding-left: 56px
  padding-right: 56px
.medium
  font-size: 16px
  height: 44px
  padding-left: 32px
  padding-right: 32px
.small
  font-size: 14px
  height: 32px
  padding-left: 16px
  padding-right: 16px

// Button with Number :::::::::::
.btn-basket
  position: relative
  &__number
    position: absolute
    font-size: 80%
    top: -10px
    right: -10px
    background-color: #FFCD5D
    border: 2px solid #ffffff
    color: $color-dark
    padding: 2px 6px 1px
    border-radius: 50%
    text-align: center

// Button Plus One :::::::::::
.plus-one-counter
  padding-left: 16px
  padding-right: 0
  justify-content: space-between
  .btn-plus-one__text
    line-height: 1
    white-space: nowrap
    padding-right: 16px
  .btn-plus-one__number
    color: $color-yellow
    background-color: $color-dark
    align-self: stretch
    border-top-right-radius: $border-radius
    border-bottom-right-radius: $border-radius
    padding-right: 14px
    padding-left: 14px
    @include btn-flex
.big.plus-one-counter
  padding-left: 24px
  .btn-plus-one__text
    padding-right: 24px
  .btn-plus-one__number
    padding-right: 20px
    padding-left: 20px

// Button Counter Replacer :::::::::::
.btn-count
  &__counter
    @include btn-flex
    //display: flex
    //flex-direction: row
    align-items: stretch
    //justify-content: center
    align-content: center
    padding-left: 0
    padding-right: 0
    border: 1px solid #eeeeee
    border-radius: $border-radius
.btn-counter-minus,.btn-counter-plus
  cursor: pointer
  align-content: center
  padding-left: 16px
  padding-right: 16px
  @include btn-flex
.btn-counter-number
  border-left: 1px solid #eeeeee
  border-right: 1px solid #eeeeee
  @include btn-flex
  align-items: stretch
  input
    border: none
    text-align: center
    padding: 0
    font-weight: 600
    width: 52px
    font-size: 16px
</style>
