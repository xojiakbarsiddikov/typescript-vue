<template>
  <div class="job-list">
    <p>Order by {{ order }}</p>
     <transition-group name="list" tag="ul">
       <li v-for="job in orderJobs" :key="job.id">
         <h2>{{ job.title }} in {{ job.location }}</h2>
         <div class="salary">
           <img src="../assets/flat,800x800,075,f.jpg" alt="">
           <p>{{ job.salary }} rupees</p>
         </div>
         <div class="description">
           <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Distinctio enim quia quidem quos reiciendis repellat, sequi soluta. Debitis, eos est, fugit nesciunt officiis quam quos, repudiandae soluta tenetur unde voluptatum.</p>
         </div>
       </li>
     </transition-group>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue'
import Job from '@/types/Job'
import OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>
    }
  },
  setup(props) {
    const orderJobs = computed(() => {
      return [...props.jobs].sort((a: Job,b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1
      })
    })

    return{ orderJobs }
  }
})
</script>

<style scoped>
  .job-list {
    max-width: 960px;
    margin: 0 auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style: none;
    background: #fff;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
    padding: 20px 0;
  }
  .salary img {
    width: 39px;
    height: 35px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move {
    transition: all 1s;
  }
</style>

