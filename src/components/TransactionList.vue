<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li
            v-for="transaction in transactions"
            :key="transaction.id"
            :class="{
                plus: transaction.amount >= 0.0,
                minus: transaction.amount <= 0.0,
            }"
        >
            <span>{{ transaction.text }}</span>
            <span>{{ transaction.amount }}</span>
            <button
                class="delete-btn"
                @click="this.$emit('onDeleteTransaction', transaction.id)"
            >
                x
            </button>
        </li>
    </ul>
</template>

<script>
export default {
    props: ["transactions"],
    emits: ["onDeleteTransaction"],
};
</script>
