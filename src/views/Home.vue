<template>
  <div>
    <section class="py-5 text-center container">
      <div class="row py-lg-5">
        <div class="col-lg-6 col-md-8 mx-auto">
          <img
            src="../assets/imgs/callout.svg"
            alt="callout"
            class="w-50"
          />
          <h2 class="font-weight-light">随心写作，自由表达{{ biggerColumnLen }}</h2>
          <p>
            <a
              href="#"
              class="btn btn-primary my-2"
            >开始写文章</a>
          </p>
        </div>
      </div>
    </section>
    <h4 class="font-weight-bold text-center">发现精彩</h4>
    <column-list :list="list"></column-list>
  </div>
</template>
<script lang="ts">
import { defineComponent, computed, onMounted } from 'vue'
import ColumnList from '@/components/ColumnList.vue'
import { useStore } from 'vuex'
import { GlobalDataProp } from '@/commons/interface'
import GlobalFn from '@/commons/global'
import { request } from '@/request'

export default defineComponent({
  name: 'Home',
  components: {
    ColumnList
  },
  setup() {
    onMounted(() => {
      store.dispatch('fetchColumns')
    })
    console.log(GlobalFn.isMobile())
    request({ url: 'myclass/myfn', methon: 'get' }).then((res) => {
      console.log(res)
    })
    const store = useStore<GlobalDataProp>()
    const currentColumn = computed(() => store.state.columns)
    const biggerColumnLen = computed(() => store.getters.biggerColumnsLen)
    return {
      list: currentColumn,
      biggerColumnLen
    }
  }
})
</script>
