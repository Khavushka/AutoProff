<template>
  <select v-model="modelValue" @change="changeCompany">
      <option disabled value="">Valg afdeling</option>
      <option v-for="option in options" :key="option.value" value="">
          {{ option.name }}
      </option>
  </select>
</template>

<script>
export default {
    name: 'my-ch',
    props: {
        modelValue: {
            type: String
        },
        options: {
            type: Array,
            default: () => []
        }
    },
    methods: {
        changeCompany(event) {
            this.$emit('update:modelValue', event.target.value)
        }
    }
}
</script>

<style scoped>

</style>