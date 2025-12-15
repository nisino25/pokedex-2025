<template>
    <div class="p-6 max-w-5xl mx-auto">
    <div class="flex flex-col md:flex-row gap-6 items-start">
        
        <!-- LEFT: Text content -->
        <div class="md:w-3/5">
            <h1 class="text-2xl font-bold mb-4">
                ポケモンバトルの基本（第3世代まで）
            </h1>

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

        <!-- RIGHT: Image -->
        <div class="md:w-2/5 flex justify-center">
            <img
                src="https://assets.st-note.com/img/1696573473604-yeIgCsnX1C.png?width=1200"
                alt="物理・特殊分類図"
                class="max-w-full rounded shadow"
            >
        </div>

    </div>
</div>

    <hr>
    <div class="p-6">
        <h1 class="text-2xl font-bold mb-6 text-center">進化の石リスト</h1>
    
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
            <div v-for="stone in stones" :key="stone.name"
                 class="bg-white shadow-md rounded-xl p-5 border border-gray-200">
                
                <h2 class="text-xl font-semibold mb-2">{{ stone.name }}</h2>
    
                <div class="text-sm text-gray-600 mb-1">
                    <span class="font-semibold">入手方法：</span>{{ stone.location }}
                </div>
    
                <div class="text-sm text-gray-600 mb-1">
                    <span class="font-semibold">値段：</span>{{ stone.price }}
                </div>
    
                <div class="text-sm text-gray-600">
                    <span class="font-semibold">対象ポケモン：</span>
                    <div class="flex flex-wrap gap-2 mt-1">
                        <span v-for="p in stone.targets" class="bg-yellow-100 text-yellow-800 text-xs py-1 px-2 rounded" :key="p">
                            {{ p }}
                        </span>
                    </div>
                </div>
    
            </div>
        </div>
    </div>
</template>

<script setup>
/* eslint-disable no-undef */

import { ref } from "vue";
const props = defineProps({
    physicalTypes: Array,
    specialTypes: Array,
    getTypeBadge: Function
});

const stones = ref([
    {
        name: "かみなりのいし",
        location: "タマムシデパート4F",
        price: "2100円",
        targets: ["ピカチュウ", "イーブイ"]
    },
    {
        name: "ほのおのいし",
        location: "タマムシデパート4F",
        price: "2100円",
        targets: ["ロコン", "ガーディ", "イーブイ"]
    },
    {
        name: "みずのいし",
        location: "タマムシデパート4F",
        price: "2100円",
        targets: ["ニョロゾ", "シェルダー", "ヒトデマン", "イーブイ", "ハスブレロ"]
    },
    {
        name: "リーフのいし",
        location: "タマムシデパート4F",
        price: "2100円",
        targets: ["クサイハナ", "ウツドン", "タマタマ", "ナッシー", "コノハナ"]
    },
    {
        name: "つきのいし",
        location: "オツキミやま / 野生のピッピ所持 / おつきみやま1F、おつきみやまB2F(隠)、ロケットだんアジトB2F、ポケモンやしき1F(隠)で拾う。2のしまでゲームコーナーの主人から貰う。",
        price: "非売品",
        targets: ["ニドリーナ", "ニドリーノ", "ピッピ", "プリン", "エネコ"]
    },
    {
        name: "たいようのいし",
        location: "6のしまのいせきのたに",
        price: "非売品",
        targets: ["クサイハナ", "ヒマナッツ"]
    }
    ])
</script>
