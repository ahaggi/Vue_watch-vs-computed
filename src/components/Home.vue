<template>
  <h3>fullNameComputed: {{ fullNameComputed }}</h3>
  <h3>fullNameProducedByWatch: {{ fullNameProducedByWatch }}</h3>

  <input type="text" placeholder="Enter a num" v-model="firstName" />
  <input type="text" placeholder="Enter a num" v-model="lastName" />
</template>

<script>
import { watch, ref, computed } from "vue";

export default {
  // https://michaelnthiessen.com/difference-between-computed-property-and-watcher/
  // https://www.netlify.com/blog/2021/01/29/deep-dive-into-the-vue-composition-apis-watch-method/
  setup() {
    const firstName = ref("");
    const lastName = ref("");

    // computed: main responsibility is to produce a result "fullNameComputed", in this case by computing some input
    const fullNameComputed = computed(() => {
      return firstName.value + " " + lastName.value;
    });

    // watch: main responsibility is to watch some variables (firstName and lastName) for changes, and handle side effects.
    const fullNameProducedByWatch = ref("");
    watch([firstName, lastName], (currentValue, oldValue) => {
      console.log(currentValue);
      console.log(oldValue);
      let [firstName, lastName] = currentValue;
      fullNameProducedByWatch.value = firstName + " " + lastName;
    });

    return { firstName, lastName, fullNameProducedByWatch, fullNameComputed };
  },
};
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
