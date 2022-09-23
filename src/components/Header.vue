<template>
  <header class="header">
    <h1 class="header__title">Notes</h1>
    <form class="header__form">
        <input type="text" placeholder="Search..." class="header__form-input" v-model="search" required>
    </form>
  </header>
</template>

<script>
export default {
    data() {
        return {
            search: ""
        }
    },
    watch: {
        search(val) {
            this.$emit("getSearch", val)
        }
    }
};
</script>

<style lang="scss" scoped>
    .header {
        padding: 15px 20px;
        box-shadow: var(--secondaryShadow);

        &__title {
            text-align: center;
            margin-bottom: 8px;
        }
        &__form {
            text-align: center;
            &-input {
                padding: 10px 15px;
                box-shadow: var(--secondaryShadow), var(--primaryShadow);
                border: 0;
                border-radius: 5px;
            }
        }
    }
</style>