<script lang="ts">
import { useExampleStore } from '../stores/exampleStore';
import { mapState } from 'pinia'
import { watch, ref } from 'vue';

//NOTE: you can disregard any composition API syntax if you stick with optionAPI (which I recommmend)
//If you want to understad how the store works here, make sure you load the <ExampleWithInteractionns> component to check the expected channges

export default {
  /*setup() {
    const store = useExampleStore()
    // This is the state read from store
    // This is showing how the store update from one component will also be reflected in other components
    watch(store, (state) => { 
      console.log(state.size)
    })
    // Setting up the local state
    const count = ref(0)
    return {
      count // This is the local state of this component
    }
  },*/
  //This is the equivalent code (data, computed, and watch) to the setup() above, but in options API
  data() {
    return {
      count: 0
    }
  },
  computed: {
    ...mapState(useExampleStore, ['size']) // Traditional way to map the store state to the local state
  },
  watch: { // This is only effective when you load with <ExampleWithInteractionns> component
    size() {
      console.log(this.size)
    }
  },
  props: {
    msg: String, // This is the props passed down from the parent component
  },
}
</script>

<!-- The following is showcasing how to use UI components from Vuetify-->
<template>
  <h3 class="ma-2">{{ msg }}</h3>

  <v-divider class="pt-1 pb-1" />

  <v-card class="ma-2 pa-4">
    <p class="pb-1">
      Left diagram shows the 2D distribution after TSNE Process, you can type any Perplexity and click button 'Click
      Here' to see the effect, the loadtime may long.
    </p>
    <p class="pb-1">
      Right graph shows the piechart of dataset showing the propotion of each class
    </p>

    <v-card-text>
      Note that this template uses Vuetify 3, where the hyperlinks in their current documentation are messed up (as they
      all are linked to Japanese translation, which is currently not available). ¯\_(ツ)_/¯ <br />
      You may either go check out the doc for <a href="https://vuetifyjs.com/en/">Vuetify 2</a>, or fix the hyperlink by
      changing the language. <br />
      For example, "https://next.vuetifyjs.com/<strong>ja</strong>/api/v-card/" won't work, but
      "https://next.vuetifyjs.com/<strong>en</strong>/api/v-card/" works.
    </v-card-text>

    <v-btn @click="count++" elevation="2">
      Have clicked this {{ count }} times
    </v-btn>
  </v-card>

</template>

<style scoped>

</style>
