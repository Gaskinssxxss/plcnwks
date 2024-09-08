<template>
    <div v-if="params" class="inset-0">
        <div @click="close" class="absolute right-10 lg:right-20 top-10">
            <button
                class="transition-transform duration-300 ease-linear transform translate-x-0 translate-y-0 hover:-translate-x-0 hover:-translate-y-1">
                <svg xmlns="http://www.w3.org/2000/svg" class="w-10 h-10 fill-che hover:fill-black" viewBox="0 0 24 24">
                    <path
                        d="M24 20.188l-8.315-8.209 8.2-8.282-3.697-3.697-8.212 8.318-8.31-8.203-3.666 3.666 8.321 8.24-8.206 8.313 3.666 3.666 8.237-8.318 8.285 8.203z" />
                </svg>
            </button>
        </div>
        <div class="h-screen flex justify-center items-center font-anton uppercase text-5xl text-gray-200">
            <h1>
                SOON
            </h1>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        params: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        close() {
            this.$emit('close');
        }
    },
}
</script>