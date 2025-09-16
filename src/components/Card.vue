<script setup>
defineProps({
    buttonText: String,
    number: String,
});

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
    <li class="card">
        <div class="card__number">
            <span>{{ number }}</span>
        </div>
        <p>
            unadmitted
        </p>
        <button class="card__button" @click="handleClick()">
            {{ buttonText }}
        </button>
    </li>
    <!-- Кнопки  появятся после переворота карточки -->
    <button class="card__check" @click="installStatus('success')">Успешно</button>
    <button class="card__check" @click="installStatus('fail')">Неудачно</button>
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

.card__check {
    display: none;
}
</style>