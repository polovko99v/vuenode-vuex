<template>
    <div id="app">
        <searchString v-model="searchText"></searchString>
        <queryForm v-model="queryObject"></queryForm>
        <input type="button" @click="showNewPassengerForm()" value=" Додати пасажира" />
        <passengerTable v-bind:passengerList="filtredPassengers" @remove="removePassenger" @update="showUpdatePassengerForm"></passengerTable>

    <passengerForm v-model="passenger" v-bind:visible="formVisible" @input="formInput"></passengerForm>

    </div>
</template>
    <script>
    import Vue from "vue";
    import passengerTable from "./components/passengerTable";
    import passengerForm from "./components/passengerForm";
    import searchString from "./components/searchString";
    import queryForm from "./components/queryForm"
    import messageSystem from "./components/messageSystem";
    import axios from "axios";
    import { mapActions } from 'vuex';

        export default {
        name:"app",
        data() {
        return{
            passengers:[
                {
                    _id: "5e80e35446ce860b8ca62027",
                    name:"Polovko",
                    destination:"USA",
                    luggageCount:5,
                    luggageWeight:10
                },
                {
                    _id: "5e80e35446ce860b8ca62028",
                    name:"Prodan",
                    destination:"Tokyo",
                    luggageCount:15,
                    luggageWeight:120
                },
                {
                    _id: "5e80e35446ce860b8ca62029",                    
                    name:"Saroz",
                    destination:"UK",
                    luggageCount:52,
                    luggageWeight:1033
                }

            ],
            passenger: {
            name: "",
            destination:"",
            luggageCount:0,
            luggageWeight:0
      },
        messagesList: [],
        formVisible: false,
        selectedIndex: -1,
        searchText: "",
        queryObject:{
          destination:""
        }
    };
},
components: {
    passengerTable,
    passengerForm,
    searchString,
    queryForm,
    messageSystem
  },
  computed: {
    filtredPassengers() {
     
      let result =  this.passengers;
      if (this.searchText) 
        result = result.filter(passenger => passenger.name.toLowerCase().includes(this.searchText.toLowerCase()));
        console.log(result)
      if (this.queryObject.destination)
        result = result.filter(passenger=> passenger.destination==this.queryObject.destination);
        console.log(result)
        return result;
    }
  },
  created(){
     this.getPassengers().then(
        passengers=> {this.passengers = passengers;}
);

  },
  
  methods: {
       ...mapActions(["showMessageForTime", "getPassengers", "showAddForm"]), 
  }
};
</script>

<style scoped>
#app {
  margin: 0;
  padding: 0;
}
</style>
