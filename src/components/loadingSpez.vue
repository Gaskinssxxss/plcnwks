<template>
    <div
        class="w-full h-full flex items-center justify-between relative overflow-hidden px-2 md:px-10 font-anton text-3xl uppercase">
        <div class="absolute" :style="loadingTextStyle">
            {{ loadingText }}
            <div class="ml-auto">{{ percent }}%</div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            percent: 0,
            loadingText: 'Loading',
            intervalId: null,
            containerWidth: 0,
        };
    },
    computed: {
        loadingTextStyle() {
            return {
                transform: `translateX(${(this.percent / 100) * this.containerWidth}px)`,
                transition: 'transform 0.1s ease-in-out',
            };
        }
    },
    mounted() {
        this.containerWidth = this.$el.clientWidth - 100;
        this.startLoading();
    },
    beforeUnmount() {
        clearInterval(this.intervalId);
    },
    methods: {
        startLoading() {
            this.intervalId = setInterval(() => {
                if (this.percent < 100) {
                    this.percent += 2;
                } else {
                    clearInterval(this.intervalId);
                    this.$emit('loadingComplete');
                }
            }, 10);
        }
    }
};
</script>
