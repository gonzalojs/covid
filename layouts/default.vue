<template>
  <div class="hero is-fullheight is-danger">
    <div class="hero-head has-text-centered margin">
      <h1 class="title is-1">Covid-19 Chile</h1>
      <h2 class="subtitle">{{date}}</h2>
    </div>

    <div class="hero-body">
      <div class="container has-text-centered">
        <nuxt />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    let event = new Date();
    let options = {
      weekday: "long",
      year: "numeric",
      month: "long",
      day: "numeric"
    };

    return {
      date: event.toLocaleDateString("es-ES", options)
    };
  },
  head() {
    return {
      link: [
        {
          rel: "stylesheet",
          href: "https://fonts.googleapis.com/css?family=Spicy+Rice&display=swap"
        }
      ]
    };
  }
};
</script>

<style>
h1, h2 {
  font-family: 'Spicy Rice', cursive;
}
.margin {
  margin-top: 100px;
}
</style>