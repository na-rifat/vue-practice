<template>
    <h3>Add new transaction</h3>
    <form
        id="form"
        role="form"
        @submit.prevent="$emit('add-transaction', form)"
    >
        <div class="form-control">
            <label for="text">Text</label>
            <input
                v-model="form.text"
                type="text"
                id="text"
                placeholder="Enter text..."
            />
        </div>
        <div class="form-control">
            <label for="amount"
                >Amount <br />
                (negative - expense, positive - income)</label
            >
            <input
                v-model="form.amount"
                type="text"
                id="amount"
                placeholder="Enter amount..."
            />
        </div>
        <button type="submit" :disabled="form.busy" class="btn">
            Add transaction
        </button>
    </form>
</template>

<script>
import Form from "vform";

export default {
    emits: ["add-transaction"],
    data: () => ({
        form: new Form({
            text: "",
            amount: "",
        }),
    }),
};
</script>
