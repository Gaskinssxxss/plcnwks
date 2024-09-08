<template>
  <div class="w-full h-screen relative flex items-center justify-center">
    <img src="@/assets/room.jpg" alt="Room"
      class="room-image w-full h-full object-cover absolute top-0 left-0 transform transition-transform duration-300 ease-in-out"
      :style="{ transformOrigin: transformOriginStyle, filter: isBlur ? 'blur(2px)' : 'blur(0px)', transform: isHovered ? (isMdScreen ? 'scale(1.6)' : 'scale(1.2)') : 'scale(1)' }">
    <div class="z-50">
      <surveySpez :params="params" @close="eventShow" />
    </div>
    <div
      class="absolute top-5 lg:top-10 left-0 lg:left-10 z-40 font-mono text-[10px]/[15px] lg:text-[5px]/[13px] whitespace-pre-wrap overflow-x-auto max-w-full text-che p-4 rounded-md"
      :style="{ filter: isBlur ? 'blur(1px)' : 'blur(0px)' }">
      <span ref="typedTexts"></span>
    </div>
    <div
      class="text-right hidden md:block absolute top-5 lg:top-10 right-12 z-40 font-mono text-[10px]/[15px] lg:text-[5px]/[13px] whitespace-pre-wrap overflow-x-auto max-w-full text-che p-4 rounded-md"
      :style="{ filter: isBlur ? 'blur(1px)' : 'blur(0px)' }">
      <span ref="typedText"></span>
    </div>
    <div class="absolute z-40 text-center" :style="{ filter: isBlur ? 'blur(4px)' : 'blur(0px)' }">
      <div class="absolute inset-0 flex justify-center items-center space-x-28 md:space-x-20">
        <div class="space-y-32 lg:space-y-28 hidden sm:block">
          <div v-if="fist" @click="survey"
            class="w-40 sm:w-32 border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Data Survey</h1>
            </button>
          </div>
          <div v-if="scnd" @click="media"
            class="w-40 sm:w-32 border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Portal Media</h1>
            </button>
          </div>
        </div>
        <div v-if="open"
          class="border-2 border-gray-200 hover:bg-gray-200 hover:text-black text-gray-200 px-2 py-1 lg:py-0 rounded-md font-anton text-3xl sm:text-xl lg:text-lg"
          @click="onClicks($event)" @mouseover="hovy" @mouseleave="outHovy">
          <button>
            <h1>Click</h1>
          </button>
        </div>
        <div v-if="closed"
          class="border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-3xl sm:text-xl lg:text-lg"
          @click="onClose()">
          <button>
            <h1>Close</h1>
          </button>
        </div>
        <div class="space-y-20 block sm:hidden -mt-10 relative -left-16 sm:left-0">
          <div v-if="fist" @click="survey"
            class="w-40 sm:w-32 border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Data Survey</h1>
            </button>
          </div>
          <div v-if="scnd" @click="media"
            class="w-40 sm:w-32 border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Portal Media</h1>
            </button>
          </div>
          <div v-if="thrd" @click="dev"
            class="w-40 sm:w-32 border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Software Dev</h1>
            </button>
          </div>
          <div v-if="fous" @click="boots"
            class="border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Bootcamp</h1>
            </button>
          </div>
        </div>
        <div class="space-y-32 lg:space-y-28 hidden sm:block">
          <div v-if="thrd" @click="dev"
            class="w-36 md:w-40 sm:w-32 border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Software Dev</h1>
            </button>
          </div>
          <div v-if="fous" @click="boots"
            class="border-2 border-gray-200 text-gray-200 hover:bg-gray-200 hover:text-black px-2 py-1 lg:py-0 rounded-md font-anton text-2xl sm:text-xl lg:text-lg">
            <button>
              <h1>Bootcamp</h1>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import surveySpez from '@/components/surveySpez.vue';
import Typed from 'typed.js';

export default {
  components: {
    surveySpez
  },
  data() {
    return {
      isHovered: false,
      transformOriginStyle: 'scale-100',
      imageRect: null,
      fist: false,
      scnd: false,
      thrd: false,
      fous: false,
      open: true,
      closed: false,
      isMdScreen: false,
      params: false,
      isBlur: false
    };
  },
  mounted() {
    this.imageRect = document.querySelector('.room-image').getBoundingClientRect();
    this.checkScreenSize();
    window.addEventListener('resize', this.checkScreenSize);
    new Typed(this.$refs.typedText, {
      strings: [`import crypto from 'crypto'
import config from './config.js'

const { secret_key, secret_iv, ecnryption_method } = config

if (!secret_key || !secret_iv || !ecnryption_method) {
  throw new Error('secretKey, secretIV, and ecnryptionMethod are required')
}

const key = crypto
  .createHash('sha512')
  .update(secret_key)
  .digest('hex')
  .substring(0, 32)
const encryptionIV = crypto
  .createHash('sha512')
  .update(secret_iv)
  .digest('hex')
  .substring(0, 16)

export function encryptData(data) {
  const cipher = crypto.createCipheriv(ecnryption_method, key, encryptionIV)
  return Buffer.from(
    cipher.update(data, 'utf8', 'hex') + cipher.final('hex')
  ).toString('base64')
}

export function decryptData(encryptedData) {
  const buff = Buffer.from(encryptedData, 'base64')
  const decipher = crypto.createDecipheriv(ecnryption_method, key, encryptionIV)
  return (
    decipher.update(buff.toString('utf8'), 'hex', 'utf8') +
    decipher.final('utf8')
  ) 
}`],
      typeSpeed: 7,
      loop: true
    });
    new Typed(this.$refs.typedTexts, {
      strings: [`const crypto = require('crypto')

function encrypt (text, key) {
  try {
    const IV_LENGTH = 16 // For AES, this is always 16
    let iv = crypto.randomBytes(IV_LENGTH)
    let cipher = crypto.createCipheriv('aes-256-cbc', Buffer.from(key), iv)
    let encrypted = cipher.update(text)
    encrypted = Buffer.concat([encrypted, cipher.final()])
    return iv.toString('hex') + ':' + encrypted.toString('hex')
  } catch (err) {
    throw err
  }
}

function decrypt (text, key) {
  try {
    let textParts = text.split(':')
    let iv = Buffer.from(textParts.shift(), 'hex')
    let encryptedText = Buffer.from(textParts.join(':'), 'hex')
    let decipher = crypto.createDecipheriv('aes-256-cbc', Buffer.from(key), iv)
    let decrypted = decipher.update(encryptedText)
    decrypted = Buffer.concat([decrypted, decipher.final()])
    return decrypted.toString()
  } catch (err) {
    throw err
  }
}

var encrypted = encrypt(password, key)
var decrypted = decrypt(encrypted, key)

console.log('Original: ' + password)
console.log('Encrypted: ' + encrypted)
console.log('Decrypted: ' + decrypted)`],
      typeSpeed: 5,
      loop: true
    });
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.checkScreenSize);
  },
  methods: {
    survey() {
      this.isBlur = true
      this.params = true
    },
    media() {
      this.isBlur = true
      this.params = true
    },
    dev() {
      this.isBlur = true
      this.params = true
    },
    boots() {
      this.isBlur = true
      this.params = true
    },
    eventShow() {
      this.params = false;
      this.isBlur = false
    },
    checkScreenSize() {
      this.isMdScreen = window.innerWidth >= 768;
    },
    hovy(event) {
      this.isHovered = true;
      this.updateTransformOrigin(event);
    },
    outHovy() {
      this.isHovered = false;
    },
    updateTransformOrigin(event) {
      const hoverRect = event.target.getBoundingClientRect();
      const centerX = hoverRect.left + hoverRect.width / 2;
      const centerY = hoverRect.top + hoverRect.height / 2;

      const originX = ((centerX - this.imageRect.left) / this.imageRect.width * 100).toFixed(2) + '%';
      const originY = ((centerY - this.imageRect.top) / this.imageRect.height * 100).toFixed(2) + '%';

      this.transformOriginStyle = `${originX} ${originY}`;
    },
    onClose() {
      if (window.innerWidth < 768) {
        this.resetAllImmediately();
        this.open = true
        this.closed = false
      } else {
        this.closeWithDelay();
      }
    },
    resetAllImmediately() {
      this.isBlur = false;
      this.params = false;
      this.fist = false;
      this.scnd = false;
      this.thrd = false;
      this.fous = false;
      this.isHovered = false;
      this.transformOriginStyle = 'scale-100';
    },

    closeWithDelay() {
      setTimeout(() => {
        this.closed = false;
        this.open = true;
        if (this.open === true) {
          setTimeout(() => {
            this.isHovered = false;
            this.transformOriginStyle = 'scale-100';
          }, 200);
        }
      }, 2500);

      setTimeout(() => { this.fist = false; }, 2000);
      setTimeout(() => { this.scnd = false; }, 1500);
      setTimeout(() => { this.thrd = false; }, 1000);
      setTimeout(() => { this.fous = false; }, 500);
    },
    onClicks(event) {
      this.open = false;
      this.closed = true;
      this.isHovered = true;

      const hoverRect = event.target.getBoundingClientRect();
      const centerX = hoverRect.left + hoverRect.width / 2;
      const centerY = hoverRect.top + hoverRect.height / 2;

      const originX = ((centerX - this.imageRect.left) / this.imageRect.width * 100).toFixed(2) + '%';
      const originY = ((centerY - this.imageRect.top) / this.imageRect.height * 100).toFixed(2) + '%';

      this.transformOriginStyle = `${originX} ${originY}`;

      setTimeout(() => {
        this.fist = true;
      }, 500);

      setTimeout(() => {
        this.scnd = true;
      }, 1000);

      setTimeout(() => {
        this.thrd = true;
      }, 1500);

      setTimeout(() => {
        this.fous = true;
      }, 2000);
    },
  }
}

</script>