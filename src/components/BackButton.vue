<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
     <section class="bg-green-50"> 
      <div class="container m-auto  py-6 px-6">
        <RouterLink
          to="/jobs"
          class="text-green-500 hover:text-green-600 flex items-center"
        >
          <i class="pi pi-arrow-left mr-4"></i> Back to Job Listings
        </RouterLink>
      </div>
    </section>
</template>