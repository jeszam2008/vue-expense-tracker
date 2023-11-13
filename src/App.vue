<script>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { useToast } from "vue-toastification";

export default {
    components: {
        Header,
        Balance,
        IncomeExpense,
        TransactionList,
        AddTransaction,
    },
    mounted() {
        this.transactions = localStorage.getItem("transactions")
            ? JSON.parse(localStorage.getItem("transactions"))
            : this.transactions;
    },
    data() {
        return {
            toast: useToast(),
            transactions: [],
        };
    },
    methods: {
        generateUniqueID() {
            return Math.floor(Math.random() * 10000000);
        },
        handleTransactionSubmit(data) {
            this.transactions.push({
                id: this.generateUniqueID(),
                text: data.text,
                amount: data.amount,
            });

            localStorage.setItem(
                "transactions",
                JSON.stringify(this.transactions)
            );
            this.toast.success("Transaction added");
        },
        handleDeleteTransaction(id) {
            this.transactions = this.transactions.filter(
                (transaction) => transaction.id !== id
            );

            localStorage.setItem(
                "transactions",
                JSON.stringify(this.transactions)
            );
            this.toast.success("Transaction deleted");
        },
    },
    computed: {
        total: function () {
            return this.transactions.reduce((accumulator, transaction) => {
                return accumulator + transaction.amount;
            }, 0.0);
        },
        income: function () {
            return this.transactions
                .filter((transaction) => transaction.amount > 0.0)
                .reduce((accumulator, transaction) => {
                    return accumulator + transaction.amount;
                }, 0.0)
                .toFixed(2);
        },
        expense: function () {
            return this.transactions
                .filter((transaction) => transaction.amount < 0.0)
                .reduce((accumulator, transaction) => {
                    return accumulator + Math.abs(transaction.amount);
                }, 0.0)
                .toFixed(2);
        },
    },
};
</script>

<template>
    <Header />
    <div class="container">
        <Balance :total="+total" />
        <IncomeExpense :income="+income" :expense="+expense" />
        <TransactionList
            :transactions="transactions"
            @onDeleteTransaction="handleDeleteTransaction($event)"
        />
        <AddTransaction
            @onTransactionSubmit="handleTransactionSubmit($event)"
        />
    </div>
</template>

<style scoped></style>
