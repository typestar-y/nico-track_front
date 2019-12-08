<template>
  <v-row justify="space-around">
    <v-col>
      <v-row align="center" justify="center">
        <v-btn @click="registerFeeling" large>
          1
        </v-btn>
      </v-row>
    </v-col>
    <v-col>
      <v-row align="center" justify="center">
        <v-btn @click="registerFeeling" large>
          2
        </v-btn>
      </v-row>
    </v-col>
    <v-col>
      <v-row align="center" justify="center">
        <v-btn @click="registerFeeling" large>
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
    async registerFeeling() {
      await this.$axios.$post('http://localhost:8083/feelings', {
        date: '2019-09-10',
        type: 1
      })
    }
  }
}
</script>

<style scoped></style>
