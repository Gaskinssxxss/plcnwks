<template>
    <div class="font-anton text-xl lg:text-base bg-black bg-opacity-50 border-2 border-black w-52">
        <div class="text-3xl lg:text-xl border-2 border-black pl-2 bg-iceBlue">
            <h1>{{ title }}</h1>
        </div>
        <div class="text-gray-300">
            <div v-if="menuI"
                class="border-2 border-black px-2 py-1 transition-transform duration-300 ease-linear transform -translate-x-0 -translate-y-0 hover:-translate-x-1 hover:-translate-y-1">
                <button>
                    <p>{{ menuI }}</p>
                </button>
            </div>
            <div v-if="menuII"
                class="border-2 border-black px-2 py-1 transition-transform duration-300 ease-linear transform -translate-x-0 -translate-y-0 hover:-translate-x-1 hover:-translate-y-1">
                <button>
                    <p>{{ menuII }}</p>
                </button>
            </div>
            <div v-if="menuIII"
                class="border-2 border-black px-2 py-1 transition-transform duration-300 ease-linear transform -translate-x-0 -translate-y-0 hover:-translate-x-1 hover:-translate-y-1">
                <button>
                    <p>{{ menuIII }}</p>
                </button>
            </div>
            <div v-if="menuIV"
                class="border-2 border-black px-2 py-1 transition-transform duration-300 ease-linear transform -translate-x-0 -translate-y-0 hover:-translate-x-1 hover:-translate-y-1">
                <div @click="pusz">
                    <button>
                        <div>
                            {{ menuIV }}
                        </div>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        title: {
            type: String,
            default: ''
        },
        menuI: {
            type: String,
            default: ''
        },
        menuII: {
            type: String,
            default: ''
        },
        menuIII: {
            type: String,
            default: '',
            required: false
        },
        menuIV: {
            type: String,
            default: '',
        },
        link: {
            type: String,
            default: '/',
        }
    },
    methods: {
        pusz() {
            this.$router.push(this.link);
        }
    }
}
</script>