<template>
  <div>
    <div>
      <b-modal
        id="delete-popup"
        v-model="visible"
        title-class="txtLeft"
        title="BootstrapVue"
        :no-close-on-esc="buttons.length === 0 ? false : true"
        :hide-footer="buttons.length === 0"
        :hide-header="showHeader === false && closable === false"
        :no-close-on-backdrop="buttons.length === 0 ? false : true"
        @hide="onHide"
      >
        <template v-slot:modal-header>
          <h5 v-show="showHeader">{{ headerContent }}</h5>
          <span
            v-show="closable"
            aria-hidden="true"
            class="close pointer"
            @click.prevent="onCrossClick"
          >×</span>
        </template>
        <div class="popup-text" v-html="content"></div>
        <template v-slot:modal-footer>
          <div
            v-for="(button, key) in buttons"
            :key="button.key"
            :class="[
              { 'popup-btn': true },
              { 'btn-class-1': buttons.length === 1 },
              { 'btn-class-2': buttons.length === 2 },
              { 'btn-class-3': buttons.length === 3 }
            ]"
          >
            <b-button
              :key="key"
              class="pointer"
              @click.prevent="onClickButton(button)"
            >{{ button.title }}</b-button>
          </div>
        </template>
      </b-modal>
    </div>
  </div>
</template>
<script>
import Vue from "vue";
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
import { BootstrapVue } from "bootstrap-vue";
Vue.use(BootstrapVue);

export default {
  props: {
    id: {
      type: String,
      default: ""
    },
    name: {
      type: String,
      default: ""
    },
    visible: {
      type: Boolean,
      default: false
    },
    content: {
      type: String,
      default: ""
    },
    buttons: {
      type: Array,
      default: () => {}
    },
    showHeader: {
      type: Boolean,
      default: false
    },
    headerContent: {
      type: String,
      default: ""
    },
    closable: {
      type: Boolean,
      default: false
    },
    noOfButton: {
      type: Number,
      default: 0
    },
    index: {
      type: Number,
      default: 0
    },
    value: {
      type: String,
      default: ""
    }
  },
  data() {
    return {};
  },
  created() {
    if (this.value) {
      this.content = this.content + " " + this.value;
    }
  },
  methods: {
    /**
     * On alert box button click
     */
    onClickButton(value) {
      this.$emit("onButtonClick", value);
    },
    /**
     * On hide alert box
     */
    onHide() {
      if (this.buttons.length === 0) {
        this.$emit("hide");
      }
    },
    /**
     * On cross button click
     */
    onCrossClick() {
      this.$emit("close");
    }
  }
};
</script>
<style scoped>
@import './style.css'
</style>
