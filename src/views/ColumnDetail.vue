<template>
  <div>
    <div class="column-detail-page w-75 mx-auto">
      <div
        class="column-info row mb-4 border-bottom pb-4 align-items-center"
        v-if="column"
      >
        <div class="col-3 text-center">
          <img
            :src="column && column.avatar"
            :alt="column.title"
            class="rounded-circle border w-100"
          />
        </div>
        <div class="col-9">
          <h4>{{ column.title }}</h4>
          <p class="text-muted">{{ column.description }}</p>
        </div>
      </div>
      <post-list :list="list"></post-list>
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue'
import { useRoute } from 'vue-router'

import PostList from '@/components/PostList.vue'
import store from '@/store'
export default defineComponent({
  name: 'ColumnDetail',
  components: {
    PostList,
  },
  setup() {
    const route = useRoute()
    const columnId = +route.params.id
    const column = computed(() => store.getters.getColumnById(columnId))
    const list = computed(() => store.getters.getPostsById(columnId))

    return {
      column,
      list,
    }
  },
})
</script>
