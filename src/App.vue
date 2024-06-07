<template>
    <Header />
    <div class="container">
        <Balance :balance="balance" />
        <IncomeExpenses :income="+income" :expense="expense" />
        <TransactionList
            :transactions="transactions"
            @remove-transaction="removeTransaction"
        />
        <AddTransaction />
    </div>
</template>

<script>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

export default {
    components: {
        Header,
        Balance,
        IncomeExpenses,
        TransactionList,
        AddTransaction,
    },
    data: () => ({
        transactions: [
            { id: 1, text: "Flower", amount: -19.99 },
            { id: 2, text: "Salary", amount: 500 },
            { id: 3, text: "Book", amount: -10.99 },
            { id: 4, text: "Camera", amount: 150 },
        ],
    }),
    computed: {
        balance() {
            return this.transactions.reduce(
                (t, transaction) => t + transaction.amount,
                0
            );
        },
        income() {
            return this.transactions
                .filter((transaction) => transaction.amount > 0)
                .reduce((t, transaction) => t + transaction.amount, 0)
                .toFixed(2);
        },
        expense() {
            return (
                this.transactions
                    .filter((transaction) => transaction.amount < 0)
                    .reduce((t, transaction) => t + transaction.amount, 0)
                    .toFixed(2) * -1
            );
        },
    },
    methods: {
        removeTransaction(id) {
            this.transactions = this.transactions.filter(
                (transaction) => transaction.id !== id
            );
        },
        addTransaction(transaction) {
            transaction.id = this.genereteUUID();
            this.transactions.push(transaction);
        },
        genereteUUID() {
            return Math.ceil(Math.random() * 1000);
        },
    },
};
</script>

