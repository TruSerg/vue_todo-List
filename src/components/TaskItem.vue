<template>
  <li class="task__list"
      v-bind:class="{done__opacity: task.completed}"
  >
    <div class="task__content">
      <a-checkbox class="task__checkbox"
                  v-model:checked="checked"
                  v-on:change="task.completed = !task.completed"
      ></a-checkbox>
      <div class="task__body">
        <div>
          <strong class="task__number">{{ index + 1 }}.</strong>
        </div>
        <span class="task__text"
              v-bind:class="{ done: task.completed }"
        >
          {{ task.title }}
        </span>
      </div>
    </div>
    <a-button
        class="task__btn"
        size="default"
        v-on:click="$emit('remove-task', task.id)"
        type="primary"
        danger ghost>
      <template #icon>
        <CloseOutlined class="icon__delete" />
      </template>
    </a-button>
  </li>
</template>

<script>
import { CloseOutlined } from '@ant-design/icons-vue';

  export default {
    data() {
      return {
        checked: false,
      }
    },

    props: {
      task: {
        type: Object,
        required: true
      },
      index: Number
    },

    components: {
      CloseOutlined
    }
  }
</script>

<style scoped>
  .done {
    text-decoration: line-through;
  }

  .done__opacity {
    opacity: 0.3;
  }

  .task__list {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 20px;
    padding: 1rem;
    max-width: 500px;
    margin: 0 auto;
    border-bottom: 1px solid #979292;
  }

  .task__content {
    display: flex;
    align-items: center;
  }

  .task__btn {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .icon__delete {
    font-size: 16px;
    color: red;
    padding: 1rem;
  }

  .task__body {
    display: flex;
  }

  .task__checkbox {
    margin-right: 2rem;
  }

  .task__text {
    margin-right: 2rem;
    text-align: center;
  }

  .task__number {
    margin-right: 1rem;
  }
</style>