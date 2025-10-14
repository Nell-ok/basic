<script setup>
import { computed } from 'vue';
import IconFail from "../icons/IconFail.vue"
import IconSuccess from "../icons/IconSuccess.vue"

const props = defineProps({
    buttonTextClose: String,
    buttonTextOpen: String,
    number: String,
    id: Number,
    word: String,
    translation: String,
    state: String,
    status: String,
});

const isClose = computed(() => props.state === 'close');
const isPending = computed(() => props.status === 'pending');
const isSuccess = computed(() => props.status === 'success');

const emit = defineEmits(['flip', 'statusChanged']);
// Функция — обработчик смены статуса
function installStatus(status) {
    emit('statusChanged', status);
}

function handleClick() {
    emit('flip');
}
</script>

<template>
    <div class="card">
        <div class="card__number">
            <span>{{ props.number }}</span>
        </div>
        <div class="card__status">
            <span v-if="!isClose && !isPending && isSuccess"><IconSuccess width="48" height="48" /></span>
            <span v-if="!isClose && !isPending && !isSuccess"><IconFail width="48" height="48" /></span>
        </div>
        <p v-if="isClose">{{ props.word }}</p>
        <p v-else>{{ props.translation }}</p>
        <template v-if="isClose && isPending">
            <button class="card__button" @click="handleClick()">
            {{ props.buttonTextClose }}
            </button>
        </template>
        <template v-else-if="!isClose && isPending">
            <div class="card__check-wrapp">
                <button class="card__check card__check--fail" @click="installStatus('success')"><IconFail width="24" height="24" /></button>
                <button class="card__check card__check--success" @click="installStatus('fail')"><IconSuccess width="24" height="24" /></button>
            </div>
        </template>
        <template v-else>
            <button class="card__button" @click="handleClick()">
            {{ props.buttonTextOpen }}
            </button>
        </template>
    </div>
</template>

<style scoped>
.card {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    width: 250px;
    height: 376px;
    padding: 28px 19px;
    background-color: var(--color-default-light);
    border-radius: 16px;
    box-shadow: 0px 0px 16px var(--shadow-card);
    box-sizing: border-box;
}

.card::after {
    position: absolute;
    content: "";
    top: 28px;
    left: 19px;
    right: 19px;
    bottom: 28px;
    border: 1px solid var(--color-light-blue);
    border-radius: 12px;
    pointer-events: none;
}

.card:hover {
    filter: drop-shadow(10px 10px 10px var(--color-filter));
}

.card__number {
    position: absolute;
    top: 20px;
    left: 35px;
    font-weight: 400;
    font-size: 14px;
    line-height: 16px;
    background-color: var(--color-default-light);
    z-index: 1;
}

.card__status {
    position: absolute;
    top: 4px;
    z-index: 1;
}

.card__button {
    position: absolute;
    padding: 0 4px;
    bottom: 19px;
    left: 80px;
    font-weight: 700;
    font-size: 12px;
    line-height: 18px;
    text-transform: uppercase;
    border: none;
    background-color: var(--color-default-light);
    z-index: 1;
    cursor: pointer;
}

.card__check-wrapp {
    display: flex;
    gap: 32px;
    padding: 0 10px;
    position: absolute;
    bottom: 19px;
    left: 79px;
    background-color: var(--color-default-light);
    z-index: 1;
}

.card__check {
    width: 24px;
    height: 24px;
    padding: 0;
    margin: 0;
    background-color: transparent;
    border: none;
    cursor: pointer;
}
</style>