<script>
export default {
  data() {
    return {
      randomName: '',
      error: false,
    };
  },
  methods: {
    async getRandomName(letter) {
      try {
        this.error = false;
        const res = await fetch('https://randomuser.me/api/');
        const json = await res.json();
        const name = json.results[0].name.first;
        if (name[0].toLowerCase() === letter.toLowerCase())
          this.randomName = name;
        else this.getRandomName(letter);
      } catch (error) {
        console.log(error);
        this.error = true;
      }
    },
  },
};
</script>

<template>
  <div class="get-name">
    <input placeholder="Letter" type="text" v-model="myInput" maxlength="1" />
    <button @click="getRandomName(myInput)">Get Name</button>
  </div>
  <div v-if="randomName">Name is: {{ randomName }}</div>
  <div v-else-if="error">Something went wrong try again</div>
  <div v-else>Enter the letter you want the name to start with</div>
</template>

<style scoped></style>
