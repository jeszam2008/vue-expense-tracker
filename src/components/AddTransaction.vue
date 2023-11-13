<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="handleSubmit()">
        <div class="form-control">
            <label for="text">Text</label>
            <input
                type="text"
                id="text"
                v-model="formData.text"
                placeholder="Enter text..."
            />
        </div>
        <div class="form-control">
            <label for="amount">
                Amount <br />
                (negative - expense, positive - income)
            </label>
            <input
                type="text"
                id="amount"
                v-model="formData.amount"
                placeholder="Enter amount..."
            />
        </div>
        <button type="submit" class="btn">Add transaction</button>
    </form>
</template>

<script>
import { useToast } from "vue-toastification";

export default {
    data() {
        return {
            toast: useToast(),
            formData: {
                text: "",
                amount: "",
            },
        };
    },
    emits: ["onTransactionSubmit"],
    methods: {
        handleSubmit() {
            if (!this.formData.text || !this.formData.amount) {
                this.toast.error("Some fields are missing.");
                return;
            }

            if (isNaN(this.formData.amount)) {
                this.toast.error("Please input valid amount.");
                return;
            }

            this.$emit("onTransactionSubmit", {
                text: this.formData.text,
                amount: parseFloat(this.formData.amount),
            });

            this.formData["text"] = this.formData["amount"] = "";
        },
    },
};
</script>
