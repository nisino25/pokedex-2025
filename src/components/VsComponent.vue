<template>
    <div class="max-w-5xl mx-auto p-6">
        <h1 class="text-2xl font-bold mb-4">ボス一覧と弱点</h1>
        <table class="min-w-full bg-white border border-gray-200">
            <thead>
                <tr class="bg-gray-100 text-center">
                    <th class="py-2 px-4">名前</th>
                    <th class="py-2 px-4">カテゴリ</th>
                    <th class="py-2 px-4">タイプ</th>
                    <th class="py-2 px-4">弱点</th>
                    <th class="py-2 px-4">最強ポケモンLv</th>
                </tr>
            </thead>
            <tbody>
                <tr
                    v-for="boss in bossList"
                    :key="boss.name"
                    class="text-center border-t border-gray-200 hover:bg-gray-50"
                >
                    <td class="py-2 px-4 font-semibold">{{ boss.name }}</td>
                    <td class="py-2 px-4">{{ boss.category }}</td>

                    <!-- 🔥 タイプを配列でバッジ表示 -->
                    <td class="py-2 px-4">
                        <span
                            v-for="t in boss.type"
                            :key="t"
                            :class="colors[t] + ' text-xs px-2 py-1 rounded mr-1'"
                        >
                            {{ t }}
                        </span>
                    </td>

                    <!-- 🔥 弱点クリック対応のバッジ -->
                    <td class="py-2 px-4">
                        <span
                            v-for="weak in boss.weaknesses"
                            :key="weak"
                            @click="$emit('selectType', weak)"
                            :class="colors[weak] + ' cursor-pointer text-xs px-2 py-1 rounded mr-1 hover:opacity-80'"
                        >
                            {{ weak }}
                        </span>
                    </td>

                    <td class="py-2 px-4">{{ boss.topLevel }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script setup>
import { ref } from "vue";

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

const bossList = ref([
    { name: "タケシ", category: "ジムリーダー", type: ["いわ"], weaknesses: ["みず","くさ","かくとう","じめん","はがね"], topLevel: 12 },
    { name: "カスミ", category: "ジムリーダー", type: ["みず"], weaknesses: ["でんき","くさ"], topLevel: 18 },
    { name: "マチス", category: "ジムリーダー", type: ["でんき"], weaknesses: ["じめん"], topLevel: 21 },
    { name: "エリカ", category: "ジムリーダー", type: ["くさ"], weaknesses: ["ほのお","こおり","どく","ひこう","むし"], topLevel: 24 },
    { name: "カゲツ", category: "ジムリーダー", type: ["どく"], weaknesses: ["じめん","エスパー"], topLevel: 25 },
    { name: "サカキ", category: "ボス", type: ["ゴースト"], weaknesses: ["じめん","エスパー","あく"], topLevel: 30 },
    
    // 通常四天王
    { name: "カンナ", category: "四天王", type: ["こおり"], weaknesses: ["ほのお","かくとう","いわ","はがね"], topLevel: 52 },
    { name: "シバ", category: "四天王", type: ["かくとう"], weaknesses: ["ひこう","エスパー","フェアリー"], topLevel: 56 },
    { name: "キクコ", category: "四天王", type: ["ゴースト","どく"], weaknesses: ["ゴースト","エスパー","あく"], topLevel: 58 },
    { name: "ワタル", category: "四天王", type: ["ドラゴン","ひこう"], weaknesses: ["こおり","ドラゴン","いわ"], topLevel: 60 },

    // 通常ライバル
    { name: "ライバル", category: "ライバル", type: ["いろいろ"], weaknesses: ["各種"], topLevel: 63 },

    // 強化後四天王
    { name: "カンナ (強化後)", category: "四天王", type: ["こおり"], weaknesses: ["ほのお","かくとう","いわ","はがね"], topLevel: 66 },
    { name: "シバ (強化後)", category: "四天王", type: ["かくとう"], weaknesses: ["ひこう","エスパー","フェアリー"], topLevel: 68 },
    { name: "キクコ (強化後)", category: "四天王", type: ["ゴースト","どく"], weaknesses: ["ゴースト","エスパー","あく"], topLevel: 70 },
    { name: "ワタル (強化後)", category: "四天王", type: ["ドラゴン","ひこう"], weaknesses: ["こおり","ドラゴン","いわ"], topLevel: 72 },

    // 強化後ライバル
    { name: "ライバル (強化後)", category: "ライバル", type: ["いろいろ"], weaknesses: ["各種"], topLevel: 75 },
]);
</script>
