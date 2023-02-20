<template>
  <button @click="handleClick('title')">order by title</button>
  <button @click="handleClick('salary')">order by salary</button>
  <button @click="handleClick('location')">order by location</button>
  <JobList :jobs="jobs" :order="order" />
  <p></p>
</template>

<script lang="ts">
import { defineComponent, reactive, ref, toRefs } from "vue";

import Job from "./Types/jobs";
import OrderTerm from "./Types/OrderTerm";
import JobList from "./components/JobList.vue";

export default defineComponent({
  name: "App",
  components: {
    JobList,
  },
  setup() {
    const jobs = ref<Job[]>([
      { id: "21", title: "Coder", location: "USA", salary: 34 },
      { id: "23", title: "prog", location: "Nja", salary: 344 },
    ]);
    const state = reactive({
      name: "line",
      age: 25 as string | number,
    });
    const order = ref<OrderTerm>("title");

    const handleClick = (term: OrderTerm) => {
      order.value = term;
    };

    return {
      jobs,
      order,
      handleClick,
      ...toRefs(state),
    };
  },
});
</script>

<style>
@import url("./assets/global.css");
</style>
