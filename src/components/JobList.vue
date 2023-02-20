<template>
  <div>Order by {{ order }}</div>
  <div>
    <ul>
      <li v-for="job in orderedJobs" :key="job.id">
        <h1>{{ job.title }}</h1>
        <p>{{ job.salary }}</p>
        <p>{{ job.location }}</p>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import Job from "../Types/jobs";
import OrderTerm from "../Types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });

    return {
      orderedJobs,
    };
  },
});
</script>
<style scoped></style>
