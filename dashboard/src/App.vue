<script setup>
import NavBar from './components/NavBar.vue'
import Hero from './components/Hero.vue'
import HomeCard from './components/HomeCard.vue'
import JobListing from './components/JobListing.vue'
</script>
<template>
  <NavBar />
  <Hero title="test title" subTitle="test subTitle" />
  <HomeCard />
  <JobListing :limit="3" />
</template>
