<template>
  <v-row justify="space-around">
    <v-col>
      <v-row align="center" justify="center">
        <v-btn @click="registerFeeling(1)" large>
          1
        </v-btn>
      </v-row>
    </v-col>
    <v-col>
      <v-row align="center" justify="center">
        <v-btn @click="registerFeeling(2)" large>
          2
        </v-btn>
      </v-row>
    </v-col>
    <v-col>
      <v-row align="center" justify="center">
        <v-btn @click="registerFeeling(3)" large>
          3
        </v-btn>
      </v-row>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'Index',
  methods: {
    async registerFeeling(type) {
      await this.$axios.$post('http://localhost:8083/feelings', {
        date: '2019-09-10',
        type
      })
    }
  }
}
</script>

<style scoped></style>
