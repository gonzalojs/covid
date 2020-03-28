<template>
  <div>
    <nav class="level">
      <div class="level-item has-text-centered">
        <div>
          <p class="title is-4">Infectados</p>
          <figure class="image has-image-centered is-96x96">
            <img class="image is-96x96" src="../assets/images/total.svg" alt="Placeholder image" />
          </figure>
          <p class="title is-3">{{total}}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="title is-4">Nuevos Hoy</p>
          <figure class="image has-image-centered is-96x96">
            <img class="image is-96x96" src="../assets/images/new.svg" alt="Placeholder image" />
          </figure>
          <p class="title is-3">{{nuevos}}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="title is-4">Recuperados</p>
          <figure class="image has-image-centered is-96x96">
            <img
              class="image is-96x96"
              src="../assets/images/recovered.svg"
              alt="Placeholder image"
            />
          </figure>
          <p class="title is-3">{{recovered}}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="title is-4">Serios</p>
          <figure class="image has-image-centered is-96x96">
            <img class="image is-96x96" src="../assets/images/serio.svg" alt="Placeholder image" />
          </figure>
          <p class="title is-3">{{serios}}</p>
        </div>
      </div>
      <div class="level-item has-text-centered">
        <div>
          <p class="title is-4">Muertes</p>
          <figure class="image has-image-centered is-96x96">
            <img class="image is-96x96" src="../assets/images/death.svg" alt="Placeholder image" />
          </figure>
          <p class="title is-3">{{deaths}}</p>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  head() {
    return {
      link: [
        {
          rel: "stylesheet",
          href:
            "https://fonts.googleapis.com/css?family=Righteous&display=swap"
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
p {
  font-family: 'Righteous', cursive;
}
.is-horizontal-center {
  justify-content: center;
}

.has-image-centered {
  margin-left: auto;
  margin-right: auto;
}
</style>
