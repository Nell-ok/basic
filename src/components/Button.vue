<script setup></script>

<template>
    <button class="button">
        <slot />
    </button>
</template>

<style scoped>
.button {
    min-width: 335px;
    padding: 16px 10px;
    font-family: var(--font);
    font-weight: 400;
    font-size: 24px;
    line-height: 36px;
    color: var(--color-default-light);
    background-color: var(--color-dark-blue);
    border: none;
    border-radius: 100px;
    cursor: pointer;
}

.button:hover {
    background-color: var(--color-hover-blue);
}
</style>