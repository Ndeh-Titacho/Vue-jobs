<script setup>
import Hero from "@/components/Hero.vue";
import Homecards from "@/components/HomeCards.vue";
import JobListings from "@/components/JobListings.vue";
</script>

<template>
    <Hero />
  <Homecards />
  <JobListings :limit="4" :showButton="true" />
</template>