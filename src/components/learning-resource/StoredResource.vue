<template>
  <ul>
    <single-resource
      v-for="resource in resources"
      :key="resource.id"
      :id="resource.id"
      :title="resource.title"
      :description="resource.description"
      :link="resource.link"
    ></single-resource>
  </ul>
</template>

<script>
import SingleResource from './SingleResource.vue';

export default {
  components: { SingleResource },
  inject: ['resources']
};
</script>

<style>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
