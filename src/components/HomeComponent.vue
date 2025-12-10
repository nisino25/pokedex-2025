<template>
    <div class="p-6 max-w-3xl mx-auto">
        <h1 class="text-2xl font-bold mb-4">ポケモンバトルの基本（第3世代まで）</h1>

        <div class="mb-6">
            <h2 class="text-xl font-semibold mb-2">物理技（タイプで決まる）</h2>
            <div class="flex flex-wrap gap-2">
                <span
                    v-for="type in physicalTypes"
                    :key="type"
                    :class="props.getTypeBadge(type)"
                    class="px-2 py-1 rounded text-sm"
                >
                    {{ type }}
                </span>
            </div>
        </div>

        <div class="mb-6">
            <h2 class="text-xl font-semibold mb-2">特殊技（タイプで決まる）</h2>
            <div class="flex flex-wrap gap-2">
                <span
                    v-for="type in specialTypes"
                    :key="type"
                    :class="props.getTypeBadge(type)"
                    class="px-2 py-1 rounded text-sm"
                >
                    {{ type }}
                </span>
            </div>
        </div>

        <p class="text-sm text-gray-600">
            ※ 第4世代（ダイヤモンド・パール）からは技ごとに物理・特殊が分かれるようになりました。
        </p>
    </div>
</template>

<script setup>
/* eslint-disable no-undef */
const props = defineProps({
    physicalTypes: Array,
    specialTypes: Array,
    getTypeBadge: Function
});
</script>
