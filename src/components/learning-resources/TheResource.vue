<template>
    <base-card>
        <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored shows</base-button>
        <base-button @click="setSelectedTab('add-resource')" :mode="addResButtonMode">Add a show</base-button>
    </base-card>
    <keep-alive>
        <component :is="selectedTab"></component>
    </keep-alive>
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
        return{
            selectedTab: 'stored-resources',
            storedResources: [
                {   
                    id: 'imdb',
                    title: 'IMDB',
                    description: "IMDb is the world's most popular and authoritative source for movie, TV and celebrity content.",
                    link: 'https://www.imdb.com/'
                },
                {   
                    id: 'friends',
                    title: 'F-R-I-E-N-D-S',
                    description: 'Follows the personal and professional lives of six twenty to thirty year-old friends living in the Manhattan borough of New York City.',
                    link: 'https://www.imdb.com/title/tt0108778/'
                },
            ],
        };
    },
    provide() {
        return {
            resources: this.storedResources,
            addResource : this.addResource,
            deleteResource: this.removeResource
        }
    },
    computed: {
        storedResButtonMode() {
            return this.selectedTab === 'stored-resources' ? null : 'flat';
        },
        addResButtonMode() {
            return this.selectedTab === 'add-resource' ? null : 'flat';
        }
    },
    methods: {
        setSelectedTab(tab) {
            this.selectedTab = tab;
        },
        addResource(title, description, url) {
            const newResource = {
                id: new Date().toISOString(),
                title: title,
                description: description,
                link: url
            };
            this.storedResources.unshift(newResource);
            this.selectedTab = 'stored-resources'
        },
        removeResource(resId) {
            const resIndex = this.storedResources.findIndex(res => res.id === resId);
            this.storedResources.splice(resIndex, 1);
        },
    }
}
</script>