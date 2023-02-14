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

<template></template>

<style scoped></style>
