<script setup>
import Hero from '@/components/Hero.vue'
import HomeCard from '@/components/HomeCard.vue'
import JobListing from '@/components/JobListing.vue'
</script>

<template>
  <div>
    <Hero title="test title" subTitle="test subTitle" />
    <HomeCard />
    <JobListing :limit="3" />
  </div>
</template>
