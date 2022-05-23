<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
      Click Me
  </div>
</template>

<script>
export default {
    props: ['delay'],
    data() {
        return {
            showBlock: false,
            timer: null,
            reactionTime: 0
        }
    },
    // The Mounted lifecycle hook
    mounted(){
        // fires when component is mounted to the dom
        console.log("Component mounted")
        setTimeout(() => {
            this.showBlock = true
            this.startTimer()
            console.log(this.delay)
        }, this.delay)

    },
    // updated hook runs when a component is updated or when values change
    updated() {
        console.log("component updated")
    },
    // Fires when the component is unmounted from dom and no longer shows
    unmounted() {
        console.log("Component Unmounted")
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {
                this.reactionTime += 10
            }, 10)
        },
        stopTimer() {
            clearInterval(this.timer)
            console.log(this.reactionTime)
            // Emit customer event with data
            this.$emit('end', this.reactionTime)
        }
    }
}
</script>

<style>
.block {
    width: 400px;
    border-radius: 20px;
    background: #0faf87;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
}
</style>