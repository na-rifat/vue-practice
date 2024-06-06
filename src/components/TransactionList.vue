<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li
            :class="transaction.amount < 0 ? 'minus' : 'plus'"
            v-for="transaction in transactions"
            :key="transaction.id"
        >
            {{ transaction.text }} <span>${{ transaction.amount }}</span
            ><button
                class="delete-btn"
                @click="$emit('remove-transaction', transaction.id)"
            >
                x
            </button>
        </li>
    </ul>
</template>

<script>
export default {
    props: {
        transactions: {
            type: Array,
            required: true,
        },
    },
    emits:[
        'remove-transaction',
    ],
    setup(props) {},
    data: () => ({}),
    methods: {},
    computed: () => {},
};
</script>
