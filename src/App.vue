<template>
  <div class="app">
    <header>
      <div class="title">
        <h1>Hayrule Jobs</h1>
      </div>
      <div class="order">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('salary')">order by salary</button>
        <button @click="handleClick('location')">order by location</button>
      </div>
    </header>
    <JobsList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import JobsList from "@/components/JobsList.vue";
import Job from './types/Job'
import OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  name: 'App',
  components: {JobsList},
  setup() {
    const jobs = ref<Job[]>([
      { title: 'farm worker', location: 'lon lon ranch', salary: 30000, id: '1' },
      { title: 'quarryman', location: 'death mountain', salary: 40000, id: '2' },
      { title: 'flute player', location: 'the lost woods', salary: 35000, id: '3' },
      { title: 'fisherman', location: 'lon lon ranch', salary: 21000, id: '4' },
      { title: 'prison guard', location: 'gerudo valley', salary: 32000, id: '5' }
    ])
    const order = ref<OrderTerm>('title')

    const handleClick = (term: OrderTerm) => {
       order.value = term
    }

    return { jobs, handleClick, order }
  }
});
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  background: antiquewhite;
}
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
header {
  text-align: center;
  padding: 32px;
}
header .order {
  padding-top: 52px;
}

button {
  margin: 0 10px;
  color: #1195c9;
  border: 3px solid #1195c9;
  background: #d5f0ff;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}
</style>
