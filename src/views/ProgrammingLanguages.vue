<template>
  <div class="whatever">
    <h1>Programming Languages</h1>
    <table>
        <tr>
        <th>Name</th>
            <th>Released year</th>
            <th>github rank</th>
            <th>pypl rank</th>
            <th>tiobe rank</th>
        </tr>
        <tr v-for="item in items">
            <td>{{ item.name }}</td>
            <td> {{ item.released_year }}</td>
            <td> {{ item.githut_rank }}</td>
            <td> {{ item.pypl_rank }}</td>
            <td> {{ item.tiobe_rank }}</td>
        </tr>
  </table>
  <form id="newPl">
    <input type="text" name="name" v-model="item.name">
    <input type="text" name="released_year" v-model="item.released_year">
    <input type="text" name="githut_rank" v-model="item.githut_rank">
    <input type="text" name="pypl_rank" v-model="item.pypl_rank">
    <input type="text" name="tiobe_rank" v-model="item.tiobe_rank">
    <button @click="saveData">send</button>
  </form>
</div>
</template>



<script>
import axios from 'axios';

export default {
    data() {
        return {
            items: [],
            api_url:"http://localhost:3004/programming-languages",
            item: {
                name: "New",
                released_year: 0,
                githut_rank: 0,
                pypl_rank: 0,
                tiobe_rank: 0
            }
        }
    },

    created() {
        console.log("hello")
        this.fetchData()
    },

    methods: {
        async fetchData() {
            console.log(this.api_url)
            axios.get(this.api_url)
            .then((response) => {
                console.log(response.data)
                this.items = response.data.data
            })
            .catch((error) => {
                console.error('Error fetching data:', error);
            });
        },
        async saveData(e) {
            e.preventDefault();
            let currentObj = this;
            let newItem = this.item;
            console.log(this.item)
            axios.post(this.api_url, newItem)
                .then(function (response) {
                    console.log(response);
                })
                .catch(function (error) {
                    console.log(error);
                });                           
        }
    }
}

</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>