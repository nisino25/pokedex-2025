<template>
    <div class="max-w-6xl mx-auto p-6">
        <h1 class="text-2xl font-bold mb-4">ポケモン図鑑</h1>

        <!-- Type filter -->
        <div class="flex gap-4 mb-4">
            <label class="mr-2 font-semibold">タイプで絞り込み:</label>
            <select v-model="selectedType" class="border px-2 py-1 rounded">
                <option value="">全て</option>
                <option v-for="type in allTypes" :key="type" :value="type">{{ type }}</option>
            </select>
            <button
                v-if="selectedType"
                @click="selectedType = ''"
                class="text-white bg-red-500 hover:bg-red-600 px-2 py-1 rounded shadow transition-colors duration-200 ml-2"
            >
                ✕
            </button>
        </div>

        <!-- Pokemon Table -->
        <table class="min-w-full bg-white border border-gray-200">
            <thead>
                <tr class="bg-gray-100 sticky top-0 z-10">
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('index')">#</th>
                    <th class="py-2 px-4">画像</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('name')">名前</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('type1')">タイプ1</th>
                    <th class="py-2 px-4">タイプ2</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('hp')">HP</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('attack')">攻撃</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('specialAttack')">特攻</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('defense')">防御</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('specialDefense')">特防</th>
                    <th class="py-2 px-4 cursor-pointer" @click="sortBy('total')">合計</th>
                </tr>
            </thead>
            <tbody>
                <tr
                    v-for="pokemon in filteredAndSortedPokemons"
                    :key="pokemon.index"
                    class="text-center border-t border-gray-200 hover:bg-gray-50"
                >
                    <td class="py-2 px-4">{{ pokemon.index }}</td>
                    <td class="py-2 px-4">
                        <img
                            :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-v/black-white/animated/${pokemon.index}.gif`"
                            :alt="pokemon.name"
                            class="w-16 h-16 mx-auto"
                        />
                    </td>
                    <td class="py-2 px-4">{{ pokemon.name }}</td>
                    <td class="py-2 px-4">
                        <span :class="getTypeBadge(pokemon.type1)">{{ pokemon.type1 }}</span>
                    </td>

                    <td class="py-2 px-4" v-if="pokemon.type2">
                        <span :class="getTypeBadge(pokemon.type2)">{{ pokemon.type2 }}</span>
                    </td>
                    <td class="py-2 px-4">{{ pokemon.hp }}</td>
                    <td class="py-2 px-4">{{ pokemon.attack }}</td>
                    <td class="py-2 px-4">{{ pokemon.specialAttack }}</td>
                    <td class="py-2 px-4">{{ pokemon.defense }}</td>
                    <td class="py-2 px-4">{{ pokemon.specialDefense }}</td>
                    <td class="py-2 px-4">{{ pokemon.total }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script setup>
// eslint-disable-next-line no-undef
const props = defineProps({
    filterType: String,
    getTypeBadge: Function
});

import { ref, computed, watch } from "vue";
import { pokemonList } from "../const/pokemonData.js";

const pokemons = ref(pokemonList);
const sortColumn = ref("index");
const sortAsc = ref(true);

// 内部選択タイプ
const selectedType = ref(props.filterType || "");

// propの変更を監視して更新
watch(
    () => props.filterType,
    (newType) => {
        selectedType.value = newType;
    }
);

const sortBy = (column) => {
    if (sortColumn.value === column) sortAsc.value = !sortAsc.value;
    else {
        sortColumn.value = column;
        sortAsc.value = false;
    }
};

// 全タイプ
const allTypes = [...new Set(pokemons.value.flatMap(p => [p.type1, p.type2]).filter(t => t))];

const filteredAndSortedPokemons = computed(() => {
    let filtered = pokemons.value;
    if (selectedType.value) {
        filtered = filtered.filter(
            p => p.type1 === selectedType.value || p.type2 === selectedType.value
        );
    }

    return [...filtered].sort((a, b) => {
        if (a[sortColumn.value] < b[sortColumn.value]) return sortAsc.value ? -1 : 1;
        if (a[sortColumn.value] > b[sortColumn.value]) return sortAsc.value ? 1 : -1;
        return 0;
    });
});
</script>
