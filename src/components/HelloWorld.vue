<template>
  <div class="main-div">
    <h1 class="head">Url Shrinker</h1>
    <input class="input" type="text" v-model="urls" />
    <button class="button" @click="urlshrink">Shorten</button>

    <div class="result">
      <h3 class="head">result</h3>
      <input class="input" type="text" v-model="shortenurl" ref="message" />
      <button @click="copyText" class="button">Copy</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => ({
    urls: "",
    shortenurl: "",
  }),
  methods: {
    copyText() {
      console.log("clicked");
      const element = this.$refs.message;
      element.select();
      element.setSelectionRange(0, 99999);
      document.execCommand("copy");
    },

    urlshrink() {
      const url = new URL("https://t.ly/api/v1/link/shorten");

      const params = {
        api_token:
          "8iazq6mgA4MQfYWhQx93iYaj0EFPrGBM7S4BL65f0rmmwYv6UTIMLr686D5N",
      };
      Object.keys(params).forEach((key) =>
        url.searchParams.append(key, params[key])
      );

      const headers = {
        "Content-Type": "application/json",
        Accept: "application/json",
      };

      let body = {
        long_url: this.urls,
      };

      fetch(url, {
        method: "POST",
        headers,
        body: JSON.stringify(body),
      })
        .then((response) => response.json())
        .then((data) => {
          this.shortenurl = data.short_url;
        });
    },
  },
};
</script>

<style scoped>
.head {
  font-size: 24px;
  text-align: center;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-weight: bold;

  color: blueviolet;
}

.input {
  width: 400px;
  height: 20px;
  margin-top: 20px;
}
.main-div {
  background-color: black;
  padding-bottom: 100px;
  padding-top: 30px;
  border: 10px solid blueviolet;
}
.result {
  margin-top: 50px;
}

.button {
  background-color: blueviolet; /* Green */
  border: none;
  color: white;
  margin-left: 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  padding-top: 2px;
  padding-bottom: 2px;
}
</style>
