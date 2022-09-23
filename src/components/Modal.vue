<template>
  <Transition name="modal">
    <div class="modal" @click="$emit('showOrClose', 'close')">
      <div class="modal__content" @click.stop>
        <h3 class="modal__content-title"> {{id ? "Edit note" : 'Add note'}} </h3>
        <form action="" class="modal__content-form" @submit.prevent="addOrChange">
          <input type="text" class="modal__content-inp" placeholder="Title" :value="title" required @input="$emit('changeTitle', $event.target.value)"/>
          <textarea class="modal__content-area" placeholder="Content" :value="desc" required  @input="$emit('changeDesc', $event.target.value)" cols="30" rows="5"></textarea>
          <div class="modal__content-btns">
            <a href="#!" class="modal__content-cancel" @click="$emit('showOrClose', 'close')">Cancel</a>
            <button class="modal__content-btn"> {{id ? "Edit" : 'Add'}} </button>
          </div>
        </form>
      </div>
    </div>
  </Transition>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: "",
    },
    desc: {
      type: String,
      default: "",
    },
    id: {
      type: String,
      default: null,
    },
  },
   methods: {
        addOrChange(){
           this.$emit('showOrClose', 'open');
           this.$emit('addOrChange', this.id);
        }
    },
};
</script>

<style lang="scss" scoped>
  .modal {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.4);
    z-index: 100;

    &-enter-active,
    &-leave-active {
        transition: 0.3s linear;
    }
    &-enter-from,
    &-leave-to {
        opacity: 0;
        transform: scale(1.2);
    }
    &-enter-to,
    &-leave-from {
        opacity: 1;
        transform: scale(1);
    }

    &__content {
      max-width: 400px;
      width: 100%;
      box-shadow: var(--secondaryShadow), var(--primaryShadow);
      padding: 30px;
      border-radius: 15px;
      background: #fff;

      &-title {
        margin-bottom: 8px;
        text-align: center;
      }

      &-form {
        display: grid;
        gap: 12px;
        place-items: center;
      }

      &-inp, &-area {
        width: 100%;
        padding: 10px;
        border-radius: 5;
        box-shadow: var(--primaryShadow);
        border: 0;
      }
      &-area {
        resize: vertical;
      }

      &-btns {
        display: flex;
        gap: 12px;
      }

      &-cancel {
        color: red;
      }

      &-btn {
        background: transparent;
        border: 0;
        font-size: 16px;
        cursor: pointer;
        color: #1a73e8;
      }
    }
  }
</style>