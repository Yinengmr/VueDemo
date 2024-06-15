<template>
  <div @click="closeOnClickModal && cancel()" class="cos-dialog" :class="{'cssHide': cssHide}" v-if="show">
    <div @click.stop="" class="dialog-main-box" :class="{'dialog-close': cssHide}">
      <div v-if="showCloseBnt" class="bnt-close" @click="cancel">
        <img src="../assets/dialog_close.png" alt="">
      </div>
      <div class="title">
        <slot name="head">
          {{ title }}
        </slot>
      </div>
      <div class="container">
        <slot></slot>
      </div>
      <div class="bnt-box">
        <slot name="bnt">
          <div class="bnt" @click="cancel">{{ cancelText }}</div>
          <div class="bnt confirm" @click="confirm">{{ confirmText }}</div>
        </slot>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
      default: '',
    },
    showCloseBnt: {
      type: Boolean,
      default: true,
    },
    closeOnClickModal: {
      type: Boolean,
      default: true,
    },
    cancelText: {
      type: String,
      default: 'Cancel',
    },
    confirmText: {
      type: String,
      default: 'confirm',
    }
  },
  data() {
    return {
      show: false,
      cssHide: false,
    }
  },
  methods: {
    open() {
      this.show = true;
    },
    close() {
      this.cssHide = true;
      setTimeout(() => {
        this.show = false;
        this.cssHide = false;
      }, 303)
    },
    cancel() {
      this.$emit("cancel");
      this.close();
    },
    confirm() {
      this.$emit("confirm")
    }
  }
}
</script>
<style scoped>
.cos-dialog {
  position: fixed;
  width: 100vw;
  height: 100vh;
  background:rgba(0, 0, 0, 0.5);
  top: 0;
  left: 0;
  animation: show-in 0.3s ease;
}
.cssHide {
  background:rgba(0, 0, 0, 0);
  animation: hide-css 0.3s ease;
}
.cos-dialog .dialog-main-box {
  padding: 0.4rem;
  min-width: 480px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  flex-shrink: 0;
  border-radius: 0.3rem;
  background: #fff;
  display: flex;
  flex-direction: column;
  animation: dialog-show-in 0.3s ease;
}
.cos-dialog .dialog-main-box.dialog-close {
  top: 55%;
  opacity: 0;
  animation: dialog-hide-css 0.3s ease;
}
.cos-dialog .dialog-main-box .title {
  text-align: center;
  margin-top: 0.16rem;
  margin-bottom: 0.34rem;
  color: #000;
  font-family: "PingFang SC";
  font-size: 0.456rem;
  font-style: normal;
  font-weight: 500;
  line-height: 0.5rem;
  text-transform: capitalize;
}
.cos-dialog .dialog-main-box .container {
  flex: 1;
  min-width: 480px;
  color: #27364b;
  font-family: "PingFang SC";
  font-size: 0.4rem;
  line-height: 0.6rem;
  font-weight: 400;
  padding: 0 0.4rem;
  padding-bottom: 0.4rem;
}
.bnt-box {
  text-align: center;
  margin-top: 0.2rem;
}
.bnt-box .bnt {
  color: #27364b;
  font-family: "PingFang SC";
  font-size: 0.4rem;
  font-style: normal;
  font-weight: 400;
  padding: 0.30rem 0;
  display: inline-block;
  min-width: 255px;
  border-radius: 0.34rem;
  margin-right: 0.3rem;
  background-color: #F6F8FC;
}
.bnt-box .bnt.confirm {
  background: linear-gradient(to right, #00EAA1, #00CEEC);
  color: #fff;
}
.bnt-box .bnt:last-child {
  margin-right: 0;
}
.bnt-close {
  position: absolute;
  right: 0.3rem;
  top: 0.3rem;
  width: 0.6rem;
  height: 0.6rem;
  padding: 0.1rem;
}
.bnt-close img {
  width: 100%;
  height: 100%;
}
@keyframes show-in {
  0% {
    background:rgba(0, 0, 0, 0);
  }

  100% {
    background:rgba(0, 0, 0, 0.5);
  }
}
@keyframes hide-css {
  0% {
    background:rgba(0, 0, 0, 0.5);
  }
  100% {
    background:rgba(0, 0, 0, 0);
  }
}
@keyframes dialog-show-in {
  0% {
    top: 55%;
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.8);  /** 叠加缩放 */
  }

  100% {
    top: 50%;
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
}
@keyframes dialog-hide-css {
  0% {
    top: 50%;
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }
  100% {
    top: 55%;
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.8);
  }
}
</style>
