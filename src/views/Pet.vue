<template>
  <div>
    <h2>{{animal.name}}({{$route.params.species}})</h2>
    <p><b>Age:</b>{{'    ' + animal.age}} years old</p>
    <p><b>Breed:</b>{{'   ' + animal.breed}}</p>
  </div>
</template>

<script>
  import { mapState } from 'vuex'

  export default {
    data() {
      return {
        animal: {}
      }
    },
    computed: {
      ...mapState([
        'cats',
        'dogs'
      ])
    },
    mounted () {
      const animal = this[this.$route.params.species][this.$route.params.id]
      this.animal = animal
    }
  }
</script>
