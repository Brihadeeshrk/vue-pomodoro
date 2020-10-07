<template>
    <v-card class="mt-8">
        <v-tabs v-model="timerType" >
            <v-tab v-for="tab in tabTitles" :key="tab">
                {{ tab }}
            </v-tab>

            <v-tabs-items v-model="timerType">
                <v-tab-item>
                    <v-card color="basil" flat class="pa-5">
                        <h1> 00:00 </h1>

                        <v-btn color="primary"> Start </v-btn>
                        <v-btn> Stop </v-btn>
                        <v-btn> Reset </v-btn>

                    </v-card>
                </v-tab-item>
            </v-tabs-items>
        </v-tabs>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            timerType: 0,
            tabTitles: ['Pomodoro', 'Short Break', 'Long Break']
        }
    }
}
</script>

<style lang="sass" scoped>
.v-card 
    width: 600px
</style>