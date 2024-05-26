<script setup lang="ts">
import { storeToRefs } from 'pinia';
import { useCommandPaletteStore } from '@/modules/command-palette/command-palette.store';
import { useRouter } from 'vue-router';

const props = withDefaults(defineProps<{ searchToolName?: string }>(), { searchToolName: () => '' });
const { searchToolName } = toRefs(props);

const commandPaletteStore = useCommandPaletteStore();
const { searchPrompt, filteredSearchResult } = storeToRefs(commandPaletteStore);

searchPrompt.value = searchToolName.value
console.log(filteredSearchResult.value)
console.log(filteredSearchResult.value["Tools"][0]["path"])

const matchedPath = filteredSearchResult.value["Tools"][0]["path"]

const router = useRouter();
router.push(matchedPath).catch(err => {
    console.error('Failed to navigate:', err);
  });

</script>

<template>
</template>

<style scoped lang="less">
</style>
