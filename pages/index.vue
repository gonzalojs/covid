<template>
  <div>
    <div class="hero is-fullheight has-background-light">
      <div class="hero-head has-text-centered ">
        <div class="container margin">
          <h1 class="title is-1 has-text-danger">Covid-19 Chile</h1>
          <h2 class="subtitle">{{date}}</h2>
        </div>
      </div>

      <div class="hero-body">
        <div class="container has-text-centered">
          <nav class="level">
            <div class="level-item has-text-centered">
              <div>
                <p class="title is-3">Infectados</p>
                <figure class="image has-image-centered is-96x96">
                  <img
                    class="image is-96x96"
                    src="../assets/images/total.svg"
                    alt="Placeholder image"
                  />
                </figure>
                <p class="title is-3">{{total}}</p>
                <progress class="progress is-danger" :value="total - recovered" :max="total"></progress>
              </div>
            </div>
            <div class="level-item has-text-centered">
              <div>
                <p class="title is-3">Nuevos Hoy</p>
                <figure class="image has-image-centered is-96x96">
                  <img
                    class="image is-96x96"
                    src="../assets/images/new.svg"
                    alt="Placeholder image"
                  />
                </figure>
                <p class="title is-3">{{nuevos}}</p>
                <progress class="progress is-warning" :value="nuevos" :max="total"></progress>
              </div>
            </div>
            <div class="level-item has-text-centered">
              <div>
                <p class="title is-3">Recuperados</p>
                <figure class="image has-image-centered is-96x96">
                  <img
                    class="image is-96x96"
                    src="../assets/images/recovered.svg"
                    alt="Placeholder image"
                  />
                </figure>
                <p class="title is-3">{{recovered}}</p>
                <progress class="progress is-success" :value="recovered" :max="total"></progress>
              </div>
            </div>
            <div class="level-item has-text-centered">
              <div>
                <p class="title is-3">Serios</p>
                <figure class="image has-image-centered is-96x96">
                  <img
                    class="image is-96x96"
                    src="../assets/images/serio.svg"
                    alt="Placeholder image"
                  />
                </figure>
                <p class="title is-3">{{serios}}</p>
                <progress class="progress is-dark" :value="serios" :max="total"></progress>
              </div>
            </div>
            <div class="level-item has-text-centered">
              <div>
                <p class="title is-3">Muertes</p>
                <figure class="image has-image-centered is-96x96">
                  <img
                    class="image is-96x96"
                    src="../assets/images/death.svg"
                    alt="Placeholder image"
                  />
                </figure>
                <p class="title is-3">{{deaths}}</p>
                <progress class="progress is-info" :value="deaths" :max="total"></progress>
              </div>
            </div>
          </nav>
        </div>
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
          href: "https://fonts.googleapis.com/css?family=Righteous&display=swap"
        },
        {
          rel: "stylesheet",
          href:
            "https://fonts.googleapis.com/css?family=Spicy+Rice&display=swap"
        }
      ]
    };
  },
  async asyncData({ $axios }) {
    const data = await $axios.$get(
      "https://thevirustracker.com/free-api?countryTotal=CL"
    );
    return {
      total: data.countrydata[0].total_cases,
      recovered: data.countrydata[0].total_recovered,
      deaths: data.countrydata[0].total_deaths,
      nuevos: data.countrydata[0].total_new_cases_today,
      serios: data.countrydata[0].total_serious_cases
    };
  }
};
</script>

<style>
h1,
h2 {
  font-family: "Spicy Rice", cursive;
}
.margin {
  margin-top: 100px;
}
p {
  font-family: "Righteous", cursive;
}
.is-horizontal-center {
  justify-content: center;
}

.has-image-centered {
  margin-left: auto;
  margin-right: auto;
}
</style>
