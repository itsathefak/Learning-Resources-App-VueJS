<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button @click="setSelectedTab('add-resources')"
    :mode="addResButtonMode"  
    >Add Resource</base-button
    >
  </base-card>
  <component :is="selectedTab"></component>
  <!-- ✅ Now correctly binds the selected component -->
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: StoredResources, // ✅ Default to StoredResources component
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'This is the Official VueJS Documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com',
        },
      ],
    };
  },
  provide() {
    return {
      resources: this.storedResources,
    };
  },
  computed:{
    storedResButtonMode(){
        return this.selectedTab === 'stored-resources' ? null : 'flat'
    },
    addResButtonMode(){
        return this.selectedTab === 'add-resources' ? null : 'flat'
    }
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab =
        tab === 'stored-resources' ? StoredResources : AddResource; // ✅ Assign the actual component
    },
  },
};
</script>
