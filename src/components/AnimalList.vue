<template>
    <div>
        <h1>Animal List</h1>

        <form @submit.prevent>
            <label for="species">Species</label>
            <input v-model="newAnimal.species" type="text" placeholder="species"><br>

            <label for="name">Name</label>
            <input v-model="newAnimal.name" type="text" placeholder="name"><br>

            <label for="birth">Birth</label>
            <input v-model="newAnimal.birth" type="text" placeholder="birth"><br>

            <select required v-model="newAnimal.sector">
                <option value="" hidden>Select your sector</option>
                <option v-for="(sector, key) in sectors" :key="key" v-bind:value="sector">{{ sector.name }}</option>
            </select><br>

            <button @click="addNewAnimal" type="submit">Add Animal</button>
        </form><hr><br>

        <table>
            <thead>
                <th>species</th>
                <th>Name</th>
                <th>Birth</th>
                <th>Sector</th>
                <th></th>
                <th></th>
                <th></th>
            </thead>
            <tbody>
                <tr v-for="(animal, key) in animals" :key="key" v-bind:class="{backgroundColor: animal.pozadina === true}" >
                    <td>{{ animal.species }}</td>
                    <td>{{ animal.name }}</td>
                    <td v-if="!animal.birth">unknown</td>
                    <td v-else>{{ animal.birth}}</td>
                    <td>{{ animal.sector.name }}</td>
                    <td><button @click="moveToTop(animal)">Move to top</button></td>
                    <td><button @click="deleteAnimal(animal)">Remove Animal</button></td>
                    <td><button @click="toggleBackground(animal)">Toggle background</button></td>
                </tr>
            </tbody>
        </table><hr><br>

        <table>
            <thead>
                <th>Sectors</th>
                <th></th>
            </thead>
            <tbody>
                <tr v-for="(sector, key) in sectors" :key="key">
                    <td>{{ sector.name }}</td>
                    <td><button @click="showAnimals(sector)">Show Animals</button></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

const sectors = [
    { name: "north"},
    { name: "east"},
    { name: "south"},
    { name: "west"}
]

export default {
  name: 'AnimalList',
  data() {
      return {
            newAnimal: {},
            sectors: sectors,
            animals: [
              {species:"monkey", name: "Srecko", birth: "10.10.2016", sector: sectors[0]},
              {species:"dog", name: "Avram", birth: "09.10.2016", sector: sectors[2], pozadina: true},
              {species:"cat", name: "Zora", birth: "", sector: sectors[1], pozadina: true},
              {species:"bear", name: "Vidoje", birth: "21.12.1985", sector: sectors[2]},
              {species:"fish", name: "Micko", birth: "11.04.2018", sector: sectors[3]},
            ]
         };
    },
  methods: {
      deleteAnimal(animal){
          console.log(animal);
          let indexOfAnimalToDelete = this.animals.indexOf(animal);
          console.log(indexOfAnimalToDelete);
          this.animals.splice(indexOfAnimalToDelete, 1);
      },

      moveToTop(animal){
          let indexOfAnimalToMoveToTop = this.animals.indexOf(animal);
          this.animals.splice(indexOfAnimalToMoveToTop, 1);
          this.animals.unshift(animal);
      },

      addNewAnimal(){
          this.animals.push(this.newAnimal);
          this.newAnimal = {};
      },

      showAnimals(sector){
        let sectorsList = [];
        this.animals.forEach(function(animal){
            if(sector == animal.sector){
                sectorsList.push(animal.species);
            }
        })

        alert("Species we have in this sector are: "+sectorsList);
      },

      isActive(animal){
          return animal.pozadina;
      },

      toggleBackground(animal){
          animal.pozadina = !animal.pozadina;
      }
  }
}
</script>
<style>
    table, tr {
        border: 1px solid #333;
    }

    .backgroundColor {
        background: lightseagreen;
    }
</style>



