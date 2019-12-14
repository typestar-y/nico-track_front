<template>
  <div>
    <v-row justify="space-around">
      <v-col v-for="type in types" :key="type.num">
        <v-row align="center" justify="center">
          <v-btn @click="registerFeeling(type.num)" large>
            <v-icon>{{ type.iconName }}</v-icon>
          </v-btn>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-btn @click="searchFeeling()"></v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <ul>
          <li v-for="(feeling, index) in feelings" :key="index">
            {{ feeling.date }} : {{ feeling.type }}
          </li>
        </ul>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data() {
    return {
      types: [
        { iconName: 'mdi-emoticon-excited-outline', num: 1 },
        { iconName: 'mdi-emoticon-outline', num: 2 },
        { iconName: 'mdi-emoticon-frown-outline', num: 3 }
      ],
      feelings: ''
    }
  },
  methods: {
    async registerFeeling(type) {
      await this.$axios.$post('http://localhost:8083/feelings', {
        date: '2019-09-10',
        type
      })
    },
    async searchFeeling() {
      const result = await this.$axios.$get('http://localhost:8083/feelings')
      this.feelings = result.feelings
    }
  }
}
</script>

<style scoped></style>
