<template>
    <div class="inc-exp-container">
        <div>
            <h4>Income</h4>
            <p id="money-plus" class="money plus">
                <span>+</span>
                <span>{{ income }}</span>
            </p>
        </div>
        <div>
            <h4>Expense</h4>
            <p id="money-minus" class="money minus">
                <span>-</span>
                <span>{{ expense }}</span>
            </p>
        </div>
    </div>
</template>

<script>
export default {
    props: ["income", "expense"],
};
</script>
