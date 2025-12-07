<template>
    <div class="flex space-x-4 bg-white shadow p-4">
        <button
            v-for="tab in tabs"
            :key="tab"
            @click="$emit('changeTab', tab)"
            :class="[
                'py-2 px-4 font-semibold transition-colors rounded',
                props.currentTab === tab
                    ? 'border-b-2 border-blue-500 text-blue-600'
                    : 'text-gray-600 hover:text-blue-500'
            ]"
        >
            {{ tab }}
        </button>
    </div>
</template>

<script setup>
// eslint-disable-next-line no-undef
const props = defineProps({
    currentTab: String
});

const tabs = ["Pokedex", "VS"];
</script>
