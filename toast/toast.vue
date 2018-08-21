<template>
  <transition name="fade">
    <div class="toastWrap" v-if="isShow" v-cloak>
      <div class="toast-content no-wrap">
        <component :is="getType()" :text="textinfo"></component>
      </div>
    </div>
  </transition>
</template>
<style lang="css">
  .fade-enter-active, .fade-leave-active {
    transition: opacity 0.5s;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .toastWrap {
    position: fixed;
    width: 100%;
    height: 100%;
    z-index: 100;
  }

  .toastWrap .toast-content {
    border-radius: 7px;
    background: rgba(0, 0, 0, 0.7);
    padding: 15px 10px;
    color: #fff;
    font-size: 14px;
    text-align: center;
    position: absolute;
    left: 50%;
    top: 50%;
    -webkit-transform: translateX(-50%) translateY(-50%);
    -moz-transform: translateX(-50%) translateY(-50%);
    -ms-transform: translateX(-50%) translateY(-50%);
    -o-transform: translateX(-50%) translateY(-50%);
    transform: translateX(-50%) translateY(-50%);
  }

  .icon-wrap {
    text-align: center;
    font-size: 14px;
  }

  .icon-img {
    width: 30px;
    height: 30px;
    line-height: 30px;
    margin: auto auto 5px;
    background: url('./img/icon-loading.png') center no-repeat;
    background-size: 80%;
    animation: myrotate 0.8s infinite linear;
  }

  .icon-text {
    white-space: nowrap;
  }

  .no-wrap {
    white-space: nowrap;
  }

  @-moz-keyframes myrotate {
    0% {
      -webkit-transform: rotate(0deg);
    }
    100% {
      -webkit-transform: rotate(360deg);
    }
  }

  @-webkit-keyframes myrotate {
    0% {
      -webkit-transform: rotate(0deg);
    }
    100% {
      -webkit-transform: rotate(360deg);
    }
  }

  @-o-keyframes myrotate {
    0% {
      -webkit-transform: rotate(0deg);
    }
    100% {
      -webkit-transform: rotate(360deg);
    }
  }

  @keyframes myrotate {
    0% {
      -webkit-transform: rotate(0deg);
    }
    100% {
      -webkit-transform: rotate(360deg);
    }
  }
</style>
<script>
  const toastText = {
    props: ['text'],
    template: `<div class="text" v-text="text"></div>`
  }
  const toastIcon = {
    props: ['text'],
    template: `<div class="icon-wrap"><div class="icon-img"></div><div class="icon-text" v-text="text"></div></div>`
  }
  export default {
    props: {
      show: {
        type: Boolean,
        default: true,
        required: false
      },
      type: {
        type: String,
        default: 'toastText', //toastText，toastIcon
        required: false
      },
      timeout: {
        type: Number,
        default: 1600,
        required: false
      },
      text: {
        type: String,
        default: '正在提交',
        required: false
      }
    },
    data: function () {
      return {
        isShow: true,
        textinfo: '',
      }
    },
    mounted: function () {
      this.showToast()
    },
    methods: {
      getType() {
        return this.type
      },
      /**
       * 如果通过外部参数传递，则显示外部参数，否则显示默认参数
       * @param text
       * @param timeout
       * @returns {Promise}
       */
      showToast(text = this.text, timeout = this.timeout) {
        this.textinfo = text
        return new Promise((reslove, reject) => {
          setTimeout(() => {
            this.isShow = false
            this.$emit('toast-cb')
            reslove()
          }, timeout)
        })
      }
    },
    components: {
      toastText,
      toastIcon
    },
  }
</script>
