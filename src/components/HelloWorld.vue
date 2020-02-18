<template>
  <div>
    <h1>Project Twitter Box Client</h1>

    <div class="box" :style="{ backgroundColor: boxColor }">
      <textarea type="text" @input="checkLength" v-model="text" />
      <button :disabled="currLength > maxLength || currLength === 0" @click="addTweet">Submit</button>
    </div>
    <h3>Used {{ currLength }} out of {{ maxLength }} characters</h3>
    <div v-for="(tweet, idx) in tweets" :key="idx">
      <h4>At {{ tweet.time.toLocaleString() }}</h4>
      <h4>{{ tweet.text }}</h4>
      <h4>____________________________</h4>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      maxLength: 20,
      currLength: 0,
      boxColor: "#b8dcdc",
      okColor: "#b8dcdc",
      redColor: "#ff0000ff",
      tweets: [],
      text: ""
    };
  },
  methods: {
    checkLength(event) {
      this.currLength = event.target.value.length;
      if (this.currLength > this.maxLength) {
        this.boxColor = this.redColor;
      } else {
        this.boxColor = this.okColor;
      }
    },
    addTweet() {
      this.tweets.push({ time: new Date(), text: this.text });
      this.text = "";
      this.currLength = 0;
    }
  },

  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box {
  width: 33%;
  background-color: #b8dcdc;
  height: 100px;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}
button {
  margin-left: 10px;
}
</style>
