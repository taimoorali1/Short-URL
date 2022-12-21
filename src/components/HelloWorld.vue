<template>
  <v-container class="text-center">

    <h1>Short URL </h1>
    <p>ShortURL is a url shortener to reduce a long link. Use our tool to shorten links and then share them, in addition
      you can monitor traffic statistics.</p>
    <br />
    <br />

    <div>
      <v-text-field label="Enter Link Here" v-model="url"></v-text-field>
    </div>

    <v-btn color="primary" elevation="2" large @click="convertToShort">Convert</v-btn>

    <div>
      <v-text-field label="Shorted URL" v-model="resulturl"></v-text-field>
    </div>

    <div class="mt-9">
      <h2>Want More? Try Premium Features!</h2>
      <p>Custom short links, powerful dashboard, detailed analytics, API, UTM builder, QR codes,<br/> browser extension, 50+
        app integrations and support. Only $14/month.
      </p>
      <v-btn color="primary" elevation="2" large >Go Premium</v-btn>
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'HelloWorld',

  data: () => ({

    url: '',
    resulturl: ''

  }),
  methods: {

    convertToShort() {
      const url = new URL(
        "https://t.ly/api/v1/link/shorten"
      );

      const params = {
        "api_token": "2n0aMBboj2ecAE9k3OO8kOiQzHIB4FG3TVUdNSU2JjSwXtq8H8lluYmGhocu",
      };
      Object.keys(params)
        .forEach(key => url.searchParams.append(key, params[key]));

      const headers = {
        "Content-Type": "application/json",
        "Accept": "application/json",
      };

      let body = {
        "long_url": this.url
      };

      fetch(url, {
        method: "POST",
        headers,
        body: JSON.stringify(body),
      }).then(response => response.json()).then(data => {
        console.log(data.short_url)
        this.resulturl = data.short_url;
      })

    }

  }
}
</script>
