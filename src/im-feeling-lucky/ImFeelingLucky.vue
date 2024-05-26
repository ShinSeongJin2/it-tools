<script setup lang="ts">
import { storeToRefs } from 'pinia';
import { useCommandPaletteStore } from '@/modules/command-palette/command-palette.store';
import { useRouter } from 'vue-router';

// #region URL로 전달된 searchToolName 검색어 얻기
const props = withDefaults(defineProps<{ searchToolName?: string }>(), { searchToolName: () => '' });
const { searchToolName } = toRefs(props);
const searchToolNameValue = searchToolName.value
// #endregion

try {

    // #region searchToolName로 가장 연관성있는 tool의 경로 얻기
    const commandPaletteStore = useCommandPaletteStore();
    const { searchPrompt, filteredSearchResult } = storeToRefs(commandPaletteStore);

    searchPrompt.value = searchToolNameValue
    if(!(filteredSearchResult.value) || !(filteredSearchResult.value["Tools"])
        || filteredSearchResult.value["Tools"].length === 0) {
        throw new Error("No tool found")
    }

    const mustRelatedToolPath = filteredSearchResult.value["Tools"][0]["path"]
    // #endregion

    // #region 가장 연관성있는 tool로 이동
    const router = useRouter()
    router.push(mustRelatedToolPath)
    // #endregion

} catch (error) {
    console.error(error)
    alert(error)
}
</script>

<template>
</template>

<style scoped lang="less">
</style>
