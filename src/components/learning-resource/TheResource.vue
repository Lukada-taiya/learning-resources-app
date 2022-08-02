<template>
  <base-card>
    <base-button
      @click="selectedTab('stored-resource')"
      :mode="activeStoredResources"
      >Stored Resources</base-button
    >
    <base-button @click="selectedTab('add-resource')" :mode="activeAddResources"
      >Add a Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedResource"></component>
  </keep-alive>
</template>

<script>
import BaseCard from '../UI/BaseCard.vue';
import AddResource from './AddResource.vue';
import StoredResource from './StoredResource.vue';
export default {
  components: { StoredResource, AddResource, BaseCard },
  provide() {
    return {
      resources: this.storedResources,
      addData: this.addResource,
      deleteRes: this.deleteRes
    };
  },
  data() {
    return {
      selectedResource: 'stored-resource',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'Best resources for vue',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn how to use google',
          link: 'https://google.com'
        }
      ]
    };
  },
  computed: {
    activeStoredResources() {
      return this.selectedResource === 'stored-resource' ? null : 'flat';
    },
    activeAddResources() {
      return this.selectedResource === 'add-resource' ? null : 'flat';
    }
  },
  methods: {
    selectedTab(tab) {
      this.selectedResource = tab;
    },
    addResource(title, desc, link) {
      const resource = {
        id: new Date().toISOString,
        title: title,
        description: desc,
        link: link
      };
      this.storedResources.unshift(resource);
      this.selectedResource = 'stored-resource';
    },
    deleteRes(id) {
      const resIndex = this.storedResources.findIndex(res => res.id === id);
      this.storedResources.splice(resIndex, 1);
    }
  }
};
</script>
