<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add Resource</base-button>
    </base-card>
    <component :is="selectedTab"></component>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';
export default {
    components: {
        StoredResources,
        AddResource
    },
    data() {
        return {
            selectedTab: 'stored-resources',
            resources: [
                {
                    id: 'official-guide',
                    title: 'Official Guide',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org'
                },
                {
                    id: 'google',
                    title: 'Google',
                    description: 'The official Vue.js documentation',
                    link: 'https://vuejs.org'
                },
            ]
        }
    },
    computed: {
       storedResButtonMode() {
           return this.selectedTab === 'stored-resources' ? null : 'flat';
       },
        addResButtonMode() {
           return this.selectedTab === 'add-resource' ? null : 'flat'
        }
    },
    provide() {
        return {
            resources: this.resources,
            addResource: this.addResource
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                title,
                description,
                link: url
            }
            this.resources.unshift(newResource);
            this.selectedTab = 'stored-resources';
        }
    }
};
</script>