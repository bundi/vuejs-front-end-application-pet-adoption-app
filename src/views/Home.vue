<template>
  <div class="home">
    <h2>Adopt a new best friend</h2>
    <button @click="togglePetForm" class="btn btn-primary">Add New Pet</button>
    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
      <b-form-group
        id="exampleInputGroup2"
        label="Pet's Name"
        label-for="exampleInput2"
      >
        <b-form-input
          id="exampleInput2"
          type="text"
          v-model="formData.name"
          placeholder="Enter name"
          required
        />
      </b-form-group>

      <b-form-group
        id="exampleInputGroup1"
        label="Pet's Age"
        label-for="exampleInput"
        >
        <b-form-input
          id="exampleInput1"
          type="number"
          v-model="formData.age"
          placeholder="Enter Age"
          required
        />
      </b-form-group>
      <b-form-group id="exampleInputGroup3" label="Species:" label-for="exampleInput3">
        <b-form-select id="exampleInput3" :options="['cats', 'dogs']" required v-model="formData.species" />
      </b-form-group>
      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
  import { mapActions } from 'vuex'
export default {
  name: 'home',
  data() {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm() {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit() {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)
      this.formData = {
        name: '',
          age: 0,
          species: null
      }
    }
  }
}
</script>
