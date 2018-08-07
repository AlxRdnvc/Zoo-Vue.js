<template>
    <div>
        <h1>Animal List</h1>
        <table>
            <thead>
                <th>Kind</th>
                <th>Name</th>
                <th>Birth</th>
                <th></th>
            </thead>
            <tbody>
                <tr v-for="(animal, key) in animals" :key="key">
                    <td>{{ animal.kind }}</td>
                    <td>{{ animal.name }}</td>
                    <td v-if="!animal.birth">unknown</td>
                    <td v-else>{{ animal.birth}}</td>
                    <td><button @click="deleteAnimal(zivotinja)">Remove Animal</button></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
  name: 'AnimalList',
  data() {
      return {
          animals: [
              {kind:"monkey", name: "Srecko", birth: "10.10.2016"},
              {kind:"dog", name: "Avram", birth: "09.10.2016"},
              {kind:"cat", name: "Zora", birth: ""},
              {kind:"bear", name: "Vidoje", birth: "21.12.1985"},
              {kind:"fish", name: "Micko", birth: "11.04.2018"},
          ]
      };
  },
  methods: {
      deleteAnimal(zivotinja){
          let indexOfAnimalToDelete = this.animals.indexOf(zivotinja);
          this.animals.splice(indexOfAnimalToDelete, 1);
      }
  }
}
</script>


