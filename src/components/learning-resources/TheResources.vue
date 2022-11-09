<template>
  <BaseCard>
    <BaseButton
      @click="setSelectedTab('StoredResources')"
      :mode="storedResButtonMode"
      >Stored Resources</BaseButton
    >
    <BaseButton @click="setSelectedTab('AddResources')" :mode="addResButtonMode"
      >Add Resource</BaseButton
    >
  </BaseCard>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
import BaseCard from '../UI/BaseCard.vue';
import StoredResources from '../learning-resources/StoredResources.vue';
import AddResources from '../learning-resources/AddResource.vue';

export default {
  components: {
    BaseButton,
    BaseCard,
    StoredResources,
    AddResources,
  },
  data() {
    return {
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn with google.',
          link: 'https://google.com',
        },
      ],
      selectedTab: 'StoredResources',
    };
  },
  provide() {
    return {
      resources: this.storedResources,
      submit: this.handleFormSubmit,
      removeItem: this.handleRemoveItem,
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'StoredResources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'AddResources' ? null : 'flat';
    },
  },
  methods: {
    setSelectedTab(tab) {
      console.log('click');
      this.selectedTab = tab;
    },
    handleFormSubmit(data) {
      const id = new Date().toISOString;
      this.storedResources.push({
        id,
        ...data,
      });
      this.setSelectedTab('StoredResources');
    },
    handleRemoveItem(id) {
      const index = this.storedResources.findIndex((res) => res.id === id);
      this.storedResources.splice(index, 1);
    },
  },
};
</script>

<style></style>
>
