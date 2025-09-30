<script setup>
import IconLike from "../icons/IconLike.vue"
const props = defineProps({
    number: Number,
});
</script>

<template>
    <div class="score">
        <span class="score__number">{{ props.number }}</span>
        <div class="score__icon">
            <IconLike />
        </div>
    </div>
</template>

<style scoped>
.score {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 13px;
    min-width: 110px;
    padding: 12px 24px;
    background-color: var(--color-light-blue);
    box-shadow: 0px 0px 4px var(--shadow);
    border-radius: 36px;
    box-sizing: border-box;
}

.score__number {
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
    color: var(--color-dark-blue);
}
</style>