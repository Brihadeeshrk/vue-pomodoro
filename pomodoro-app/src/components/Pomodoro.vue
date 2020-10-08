<template>
    <v-card class="mt-8">
        <v-tabs v-model="CurrentTimer" grow @change="changeCurrentTimer">
            <v-tab v-for="timer in timers" :key="timer.name">
                {{ timer.name }}
            </v-tab>
        </v-tabs>
        <v-card flat class="pa-5 d-flex flex-column justify-center align-center">
            <h1 class="time"> {{displayMinutes}} : {{displaySeconds}} </h1>
                        
            <div class="button-group">
                <v-btn color="primary" @click="start"> <v-icon left small>mdi-play-circle-outline</v-icon> Start </v-btn>
                <v-btn color="error" @click="stop"> <v-icon left small>mdi-stop-circle-outline</v-icon> Stop </v-btn>
                <v-btn @click="reset(timers[CurrentTimer].minutes)" :disabled="isRunning"> <v-icon left small>mdi-restart</v-icon> Reset </v-btn>
            </div>

        </v-card>
        <SettingsDialog :dialog="dialog" :closeDialog="closeDialog" :save="save" :timers="timers" />
        
    </v-card>
</template>

<script>
import SettingsDialog from './SettingsDialog.vue'

export default {
    components: {
        SettingsDialog
    },
    props: {
        dialog: {
            type: Boolean,
            require: true
        },
        closeDialog: {
            type: Function,
            require: true
        },
    },
    data() {
        return {
            timerInstance: null,
            CurrentTimer: 0,
            timers: [
                {
                    name: 'Pomodoro',
                    minutes: 25
                },
                {
                    name: 'Short Break',
                    minutes: 5
                },
                { 
                    name: 'Long Break',
                    minutes: 10
                }
            ],
            totalSeconds: 25 * 60,
            isRunning: false,
        }
    },
    computed: {
        displayMinutes() {
            const minutes = Math.floor(this.totalSeconds / 60)

            return this.formatTime(minutes)
        },
        displaySeconds() {
            const seconds = this.totalSeconds % 60
            
            return this.formatTime(seconds)
        }
    },
    methods: {
        formatTime(time) {
            if(time < 10) {
                return '0' + time
            }
            return time.toString()
        },
        start() {
            this.stop(),
            this.isRunning = true
            this.timerInstance = setInterval(() => {
                if(this.totalSeconds <= 0) {
                    this.stop()
                    return
                }
                this.totalSeconds -= 1
            }, 1000)
        },
        stop() {
            this.isRunning = false
            clearInterval(this.timerInstance)
        },
        reset(minutes) {
            this.stop(),
            this.totalSeconds = minutes * 60
        },
        changeCurrentTimer(num) {
            console.log(num)
            this.CurrentTimer = num
            this.reset(this.timers[num].minutes)
        },
        save(updatedTimers) {
            this.timers = this.timers.map((timer, i) => {
                return { ...timer, minutes: parseInt(updatedTimers[i])}
            }),
            this.closeDialog()
        }
    }
}
</script>

<style lang="sass" scoped>
.v-card 
    width: 600px

.v-btn 
    margin: 0 5px

.time
    font-size: 80px
    font-weight: 400
    text-align: center

</style>