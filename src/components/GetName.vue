<script>
export default {
  data() {
    return {
      randomName: '',
      error: false,
      user: {},
    };
  },
  methods: {
    async getRandomName(letter) {
      try {
        this.error = false;
        const res = await fetch('https://randomuser.me/api/');
        const json = await res.json();
        const userObject = json.results[0];
        const name = userObject.name.first;
        if (name[0].toLowerCase() === letter.toLowerCase()) {
          this.randomName = name;
          this.user = userObject;
        } else this.getRandomName(letter);
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

<style scoped>
button {
  font-weight: bold;
  height: 85%;
  border-radius: 0.5rem;
  border: white solid 1px;
}
input {
  font-weight: bold;
  font-size: 30px;
  width: 6rem;
  border-radius: 0.5rem;
  border: white solid 1px;
  text-align: center;
}
.get-name {
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  height: 3rem;
  gap: 1rem;
}
</style>
