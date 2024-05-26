<script setup lang="ts">
const props = withDefaults(defineProps<{ searchToolName?: string }>(), { searchToolName: () => '' });
const { searchToolName } = toRefs(props);

alert(`TODO: 검색 관련 로직이 실행되고, 해당 Tool로 이동되어야 함. 현재 검색어: ${searchToolName.value}`)
</script>

<template>
</template>

<style scoped lang="less">
</style>
