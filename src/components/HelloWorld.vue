<template>
  <div>
    <h1>Project Twitter Box Client</h1>

    <div class="outer-box">
      <div class="inner-box">
        <textarea
          v-model="tweet"
          @input="checkCharacterLength"
          type="text"
          :maxlength="maxCharacters"
        />
        <button @click="postTweet" :disabled="!disableSubmit">Submit</button>
      </div>

      <div class="input-info" :class="{ 'input-warning': redWarningText }">
        <p v-show="typing">Characters remaining: {{ charactersRemaining }}</p>
      </div>
    </div>

    <article class="tweets" v-for="(tweet, index) in tweets" :key="index">
      <p>{{ tweet }}</p>
    </article>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      tweets: [],
      tweet: "",
      maxCharacters: 50,
      charactersRemaining: null,
      typing: false,
      warning: false,
    };
  },
  methods: {
    checkCharacterLength() {
      this.typing = false;

      if (this.tweet.length >= 1) {
        this.typing = true;
        this.charactersRemaining = this.maxCharacters - this.tweet.length;
      }
    },

    postTweet() {
      this.tweets.push(this.tweet);
      this.tweet = "";
      this.typing = false;
    },
  },

  computed: {
    redWarningText() {
      return this.charactersRemaining < 10 ? !this.warning : this.warning;
    },

    disableSubmit() {
      return this.maxCharacters - this.tweet.length;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.outer-box {
  width: 33%;
  background-color: #b8dcdc;
  height: 100px;
  margin: 0 auto;
  display: grid;
  grid-template: 2fr 1fr / 1fr;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}
.inner-box {
  /* border: 1px solid red; */
  padding-top: 0.5rem;
}
.inner-box textarea {
  height: 100%;
}

button {
  margin-left: 10px;
}
button:disabled {
  cursor: not-allowed;
  pointer-events: all;
}

.input-info {
  /* border: 1px solid orange; */
}
.input-info p {
  /* border: 1px solid black; */
  align-self: end;
}
.input-warning p {
  color: red;
}

.tweets {
  width: 33%;
  background-color: #b8dcdc;
  height: 100px;
  margin: 2rem auto;
  display: flex;
  align-items: center;
  padding: 1rem;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1),
    0 10px 10px -5px rgba(0, 0, 0, 0.04);
}
</style>
