<template>
  <div class="container-fluid p-0 m-0">
    <b-navbar type="dark" variant="dark">
      <b-navbar-nav>
        <div>
          <b-nav-item href="#">Url Shortener</b-nav-item>
        </div>

        <!-- Navbar dropdowns -->
      </b-navbar-nav>
      <button class="button2">Sign up</button>
    </b-navbar>

    <div class="main-div">
      <h1 class="head">Paste the URL to be shortened</h1>
      <input
        class="input"
        type="text"
        v-model="urls"
        placeholder="Enter Your Url Here"
      />
      <button class="button" @click="urlshrink">Shorten</button>

      <div class="result">
        <h3 class="head">Result</h3>
        <input
          class="input"
          readonly
          placeholder="Shortened Url will appear here"
          type="text"
          v-model="shortenurl"
          ref="message"
        />
        <button @click="copyText" class="button">Copy</button>
      </div>
    </div>

    <div class="container card-area">
      <div class="card mt-3">
        <h6 class="head2">
          Easy <v-icon color="#ffff" size="30">mdi-thumb-up</v-icon>
        </h6>
        <p>Short and Easy Way to Shorten Url</p>
      </div>
      <div class="card mt-3">
        <h6 class="head2">
          Shortened <v-icon color="#ffff" size="30">mdi-text-short</v-icon>
        </h6>
        <p>Any Links can be shortened with our algorithms</p>
      </div>
      <div class="card mt-3">
        <h6 class="head2">
          Secure
          <v-icon color="#ffff" size="30">mdi-account-lock</v-icon>
        </h6>
        <p>With high level encryption your urls are always safe and secure</p>
      </div>
    </div>

    <div class="container card-area">
      <div class="card mt-3">
        <h6 class="head2">
          Statistics
          <v-icon color="#ffff" size="30">mdi-chart-bell-curve</v-icon>
        </h6>
        <p>You can see stats on how many users have used shortened url</p>
      </div>
      <div class="card mt-3">
        <h6 class="head2">
          Reliable <v-icon color="#ffff" size="30">mdi-charity</v-icon>
        </h6>
        <p>
          We delete any links which is a potential threat to malware or viruses
        </p>
      </div>
      <div class="card mt-3">
        <h6 class="head2">
          Devices <v-icon color="#ffff" size="30">mdi-cellphone-link</v-icon>
        </h6>
        <p>Compatible with smartphones tablets and desk top</p>
      </div>
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
.card-area {
  display: flex;
  justify-content: space-evenly;
  margin-top: 20px;
  flex-wrap: wrap;
}
input:focus {
  outline: none;
}
.navbar {
  background-color: black;
  display: flex;
  justify-content: space-between;
}
.head {
  font-size: 24px;
  margin-bottom: 20px;
  text-align: center;

  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-weight: bold;

  color: black;
}
.head2 {
  font-size: 24px;
  text-align: center;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-weight: bold;

  color: white;
}

.input {
  width: 400px;
  height: 20px;
  margin-top: 20px;
  border: none;
  border-bottom: 2px solid black;
}
.card {
  box-shadow: 1px 2px 3px 4px rgba(20, 20, 20, 0.4);
  height: 120px;
  width: 250px;
  background-color: #212529;

  color: white;
  border: none;
}

.main-div {
  padding-bottom: 100px;
  padding-top: 30px;
}
.result {
  margin-top: 50px;
}
p {
  padding-left: 5px;
  padding-right: 5px;
  padding-bottom: 5px;
}

.button {
  background-color: black; /* Green */
  border: none;
  color: white;
  margin-left: 30px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 20px;
  padding-top: 5px;
  padding-left: 10px;
  padding-right: 10px;
  padding-bottom: 5px;
}

.button2 {
  margin-right: 10px;
  background-color: blueviolet; /* Green */
  border: none;
  color: white;
  margin-left: 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  padding-top: 5px;
  padding-bottom: 5px;
  padding-left: 10px;
  padding-right: 10px;
}
body {
  margin: 0px;
}
</style>
