<template>
  <div class="contains">
    <div class="row">
      <div v-for="column in columnList" :key="column.id" class="col-4 mb-4">
        <div class="card h-100 shadow-sm">
          <div class="card-body">
            <img
              :src="column.avatar"
              class="rounded-circle border border-light my-3 text-center"
              :alt="column.title"
            />
            <h5 class="card-title text-center">{{ column.title }}</h5>
            <p class="card-text text-start">
              {{ column.description }}
            </p>
            <router-link :to="`/column/${column.id}`" class="btn btn-outline-primary"
              >前往专栏</router-link
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent, PropType, computed } from "vue";
export interface ColumnProps {
  id: number;
  title: string;
  avatar?: string;
  description: string;
}
export default defineComponent({
  name: "ColumnList",
  props: {
    list: {
      type: Array as PropType<ColumnProps[]>,
      required: true,
    },
  },
  setup(props) {
    const columnList = computed(() => {
      return props.list.map((column) => {
        if (!column.avatar) {
          column.avatar = require("@/assets/imgs/noavatar_middle.gif");
        }
        return column;
      });
    });

    return {
      columnList,
    };
  },
});
</script>
<style scoped>
.card-body img {
  width: 50px;
  height: 50px;
}
</style>
