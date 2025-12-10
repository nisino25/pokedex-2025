<template>
    <div class="min-h-screen bg-gray-50">
        <!-- Top Tabs -->
        <TabMenu :currentTab="currentTab" @changeTab="currentTab = $event" />

        <!-- Main Content -->
        <div>
            <HomeComponent
                v-if="currentTab === 'Home'"
                :getTypeBadge="getTypeBadge"
                :physical-types="physicalTypes"
                :special-types="specialTypes"
            />
            <PokemonPokedex
                v-if="currentTab === 'Pokedex'"
                :filterType="selectedType"
                :getTypeBadge="getTypeBadge"
                :physical-types="physicalTypes"
                :special-types="specialTypes"
            />
            <VsComponent
                v-else-if="currentTab === 'VS'"
                @selectType="handleWeaknessClick"
            />
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";
import TabMenu from "./components/TabMenu.vue";
import HomeComponent from "./components/HomeComponent.vue";
import PokemonPokedex from "./components/PokemonPokedex.vue";
import VsComponent from "./components/VsComponent.vue";

const currentTab = ref("Pokedex");
const selectedType = ref("");

// VSからタイプクリックでPokedexへジャンプ
const handleWeaknessClick = (type) => {
    selectedType.value = type;
    currentTab.value = "Pokedex";
};

// ---------- Badge Function (parent) ----------
function getTypeBadge(type) {
    const colors = {
        ノーマル: "bg-gray-300 text-black",
        ほのお: "bg-red-500 text-white",
        みず: "bg-blue-500 text-white",
        くさ: "bg-green-500 text-white",
        でんき: "bg-yellow-400 text-black",
        こおり: "bg-cyan-300 text-black",
        かくとう: "bg-orange-700 text-white",
        どく: "bg-purple-500 text-white",
        じめん: "bg-amber-600 text-white",
        ひこう: "bg-indigo-300 text-black",
        エスパー: "bg-pink-500 text-white",
        むし: "bg-lime-600 text-white",
        いわ: "bg-yellow-700 text-white",
        ゴースト: "bg-violet-700 text-white",
        ドラゴン: "bg-indigo-700 text-white",
        あく: "bg-gray-800 text-white",
        はがね: "bg-gray-500 text-white",
        フェアリー: "bg-pink-300 text-black",
    };


    return (
        "px-1 py-1 rounded text-xs font-bold inline-block " +
        (colors[type] || "bg-gray-200 text-black")
    );
}

const physicalTypes = [
    "ノーマル",
    "かくとう",
    "どく",
    "じめん",
    "ひこう",
    "むし",
    "いわ",
    "ゴースト",
    "はがね"
];

const specialTypes = [
    "ほのお",
    "みず",
    "でんき",
    "くさ",
    "こおり",
    "エスパー",
    "ドラゴン",
    "あく"
];
</script>
