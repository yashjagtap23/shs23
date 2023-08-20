<template>
    <div>
        <h1>Pomodoro Timer</h1>
        <div class="timer">
            <p>{{ formatTime }}</p>
        </div>
        <div class="controls">
            <button @click="startTimer" :disabled="isRunning">Start</button>
            <button @click="pauseTimer" :disabled="!isRunning">Pause</button>
            <button @click="resetTimer">Reset</button>
        </div>
    </div>
</template>

<script>export default {
        data() {
            return {
                isRunning: false,
                time: 25 * 60, // 25 minutes in seconds
                timer: null
            };
        },
        computed: {
            formatTime() {
                const minutes = Math.floor(this.time / 60);
                const seconds = this.time % 60;
                return `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
            }
        },
        methods: {
            startTimer() {
                if (!this.isRunning) {
                    this.timer = setInterval(() => {
                        if (this.time > 0) {
                            this.time--;
                        } else {
                            clearInterval(this.timer);
                            this.isRunning = false;
                            alert('Time is up! Take a break.');
                        }
                    }, 1000);
                    this.isRunning = true;
                }
            },
            pauseTimer() {
                if (this.isRunning) {
                    clearInterval(this.timer);
                    this.isRunning = false;
                }
            },
            resetTimer() {
                clearInterval(this.timer);
                this.isRunning = false;
                this.time = 25 * 60; // Reset to 25 minutes
            }
        }
    };</script>

<style>

    .timer {
        font-size: 2em;
    }

    .controls button {
        font-size: 1em;
        margin: 5px;
    }
</style>
