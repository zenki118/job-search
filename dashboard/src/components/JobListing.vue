<script setup>
import { ref, onMounted, defineProps } from 'vue'
import JobsListingCard from './JobsListingCard.vue'
import { RouterLink } from 'vue-router'
import axios from 'axios'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'

defineProps({
  limit: {
    type: Number,
    default: 6,
  },
  showViewAll: {
    type: Boolean,
    default: true,
  },
})

const jobs = ref([])
const isLoading = ref(false)

onMounted(async () => {
  try {
    isLoading.value = true
    const response = await axios.get('http://localhost:8000/jobs')
    jobs.value = response.data
  } catch (error) {
    console.error('Error fetching jobs:', error)
  } finally {
    isLoading.value = false
  }
})
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">Browse Jobs</h2>
    </div>
    <div v-if="isLoading" class="flex justify-center my-10">
      <PulseLoader :loading="isLoading" color="#22c55e" size="15px" margin="5px" />
    </div>
    <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
      <JobsListingCard
        v-for="job in jobs.slice(0, limit || jobs.length)"
        :key="job.id"
        :job="job"
      />
    </div>
  </section>

  <section v-if="jobs.length > limit && showViewAll" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>
