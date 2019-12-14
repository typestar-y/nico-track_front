<template>
  <div>
    <v-alert v-show="errorMessage" dense outlined type="error">
      {{ errorMessage }}
    </v-alert>
    <v-alert v-show="isSuccess" dense outlined type="info">
      Feelingを登録しました
    </v-alert>
    <v-row justify="space-around">
      <v-text-field v-model="userName" label="ユーザ名" />
    </v-row>
    <v-row justify="space-around">
      <v-col v-for="type in types" :key="type.num">
        <v-row align="center" justify="center">
          <v-btn
            @click="registerFeeling(type.num)"
            :color="type.color"
            fab
            large
          >
            <v-icon color="white" x-large>{{ type.iconName }}</v-icon>
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
            {{ feeling.date }} : {{ feeling.type }}: {{ feeling.userName }}
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
      userName: '',
      isSuccess: '',
      errorMessage: '',
      types: [
        {
          iconName: 'mdi-emoticon-excited-outline',
          num: 1,
          color: 'lime lighten-3'
        },
        { iconName: 'mdi-emoticon-outline', num: 2, color: 'grey lighten-3' },
        {
          iconName: 'mdi-emoticon-frown-outline',
          num: 3,
          color: 'blue-grey lighten-3'
        }
      ],
      feelings: ''
    }
  },
  methods: {
    async registerFeeling(type) {
      this.isSuccess = ''
      this.errorMessage = ''
      await this.$axios
        .$post('http://localhost:8083/feelings', {
          date: this.$moment().format(),
          type,
          user: this.userName
        })
        .then((response) => {
          this.isSuccess = true
        })
        .catch((error) => {
          this.errorMessage = error.response.data
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
