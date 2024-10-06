<script setup></script>

<template>
  <div class="bg-secondary justify-content-around px-5">
    <headerComponent />
    <navBar />
    <main class="row bg-white p-0 m-0">
      <!-- slot below to accept nuxt routed content i believe-->
      <slot></slot>
    </main>
    <footerComponent />
  </div>
</template>
