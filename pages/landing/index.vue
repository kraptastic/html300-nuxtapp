<script setup>
import { ref, onMounted } from "vue";

import card from "@/components/card.vue";

//store page heading
const pageHeading = ref("Customer Experience Slideshow");

// store carousel image locations, classes and alt ids in object
const imageDetails = ref([
  {
    dir: "/tolmie_lookout.jpg",
    class: "carousel-item active",
    altText: "view of mt rainier from tolmie fire lookout",
  },
  {
    dir: "/stillaguamish_south_fork.jpg",
    class: "carousel-item",
    altText: "rapid autumn waters in stillaguamish south fork river",
  },
  {
    dir: "/rainier_lake.jpg",
    class: "carousel-item",
    altText: "alpine lake in mt rainier national park",
  },
]);

// store pokemon empty array with ref to make dynamic
const jsonInfo = ref([]);
onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    jsonInfo.value = await response.json();
    console.log(jsonInfo.value);
  } catch (error) {
    console.log(error);
  }
});

//store state variable for interactive css change
const clickedState = ref(true);
</script>

<template>
  <div class="col-lg-8 col-xs-10 p-2 text-center">
    <!-- landing page content area-->

    <h1 class="">{{ pageHeading }}</h1>

    <div id="carouselExample" class="carousel slide">
      <!-- image carousel with button controls below -->
      <div
        class="carousel-inner p-4"
        data-bs-toggle="tooltip"
        data-bs-placement="top"
        data-bs-title="Use arrows to cycle slideshow"
      >
        <div :class="i.class" v-for="i in imageDetails" :key="i.dir">
          <!-- iterate over object to create carousel images-->
          <img :src="i.dir" class="d-block w-100" :alt="i.altText" />
        </div>
      </div>
      <button
        class="carousel-control-prev"
        type="button"
        data-bs-target="#carouselExample"
        data-bs-slide="prev"
      >
        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Previous</span>
      </button>
      <button
        class="carousel-control-next"
        type="button"
        data-bs-target="#carouselExample"
        data-bs-slide="next"
      >
        <span class="carousel-control-next-icon" aria-hidden="true"></span>
        <span class="visually-hidden">Next</span>
      </button>
    </div>
  </div>
  <div class="col-lg-4 col-xs-10 p-2 text-center">
    <!-- sidebar content -->
    <h4 class="p-4">
      Our guided charters bring you closer to nature than you ever thought
      possible.
    </h4>
    <div class="jumbotron jumbotron-fluid p-4">
      <!-- this jumbotron pushes the big conversion right away -->
      <h1 class="display-6">Book Your Trip Today!</h1>
      <p class="lead">
        Locations include Idaho, Oregon, Washington, and international Pacific
        Ocean waters.
      </p>
      <hr class="my-4" />
      <p>Select a trip based on location and available dates.</p>
      <p class="lead">
        <a
          class="btn btn-primary btn-lg"
          href="#/Contact"
          role="button"
          data-bs-toggle="tooltip"
          data-bs-placement="bottom"
          data-bs-title="Click here to book"
          >Book Your Trip</a
        >
      </p>
    </div>
  </div>
  <!-- api feature content container below -->
  <div class="col-12 px-4 pb-4 text-center justify-content-around">
    <h5>information on all previous customers available</h5>
    <button class="btn-warning" @click="clickedState = !clickedState">
      Click here to show all previous customer reviews
    </button>
    <ul>
      <li v-if="clickedState" v-for="user in jsonInfo" :key="user.id">
        <card
          :name="user.name"
          :user="user.username"
          :email="user.email"
          :phone="user.phone"
        ></card>
      </li>
      <li v-else class=".d-none"></li>
    </ul>
  </div>
</template>

<style scoped>
* {
  list-style-type: none;
}
</style>
