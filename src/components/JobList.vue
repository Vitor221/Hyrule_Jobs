<template>
    <div class="job-list">
        <p>Ordenado por {{ order }}</p>
        <transition-group name="list" tag="ul">
            <li v-for="job in orderedJobs" :key="job.id">
                <h2>{{ job.title }} in {{ job.location }}</h2>
                <div class="salario">
                    <img src="../assets/rupee.svg">
                    <p>{{ job.salary }} rupees</p>
                </div>
                <div class="descricao">
                    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Fuga voluptas quo adipisci obcaecati possimus recusandae esse! Eius tempora quam, necessitatibus recusandae veritatis veniam, reprehenderit accusamus magni doloribus, quibusdam quos quis!</p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from 'vue';
import Job from '@/types/Job';
import OrderTerm from '@/types/OrderTerm';

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
        const orderedJobs = computed(() => {
            return [...props.jobs].sort((a: Job, b: Job) => {
                return a[props.order] > b[props.order] ? 1 : -1
            }); 
        })

        return { orderedJobs }
    }
})
</script>

<style scoped>
.job-list {
    max-width: 960px;
    margin: 40px auto;
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
.salario {
    display: flex;
}
.salario img {
    width: 30px;
}
.salario p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
}
.list-move {
    transition: all 1s;
}
</style>