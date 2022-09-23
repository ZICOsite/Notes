<template>
  <div class="notes__item">
    <h3 class="notes__item-title">{{ note.title }}</h3>
    <span class="notes__item-date"> {{ note.date }} </span>
    <p class="notes__item-desc">{{ note.desc }}</p>
    <div class="notes__item-control">
      <a href="#" class="notes__item-edit" @click.prevent="$emit('edit', note.id)">
        <img src="@/assets/img/edit.svg" alt="" />
        edit
      </a>
      <a href="#" class="notes__item-delete" @click.prevent="$emit('remove', note.id)">
        <img src="@/assets/img/delete.svg" alt="" />
        delete
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      default: {
        title: "",
        desc: "",
        date: "",
        id: 0,
      },
    },
  },
};
</script>

<style lang="scss" scoped>
.notes__item {
  display: grid;
  gap: 5px;
  padding: 20px;
  border-radius: 15px;
  box-shadow: var(--secondaryShadow), var(--primaryShadow);
  &-date {
    font-size: 14px;
    color: #999;
  }
  &-control {
    display: flex;
    justify-content: flex-end;
    column-gap: 30px;
  }
  &-edit,
  &-delete {
    display: flex;
    align-items: center;
    gap: 8px;
  }
}
</style>