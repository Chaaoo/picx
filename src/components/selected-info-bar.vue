<template>
  <div class="selected-info-bar-box" v-if="userConfigInfo.selectedRepos">
    <span class="info-item">
      仓库：<el-tag size="mini">{{ userConfigInfo.selectedRepos }}</el-tag>
    </span>
    <span class="info-item"
          v-if="userConfigInfo.selectedBranch"
    >
      分支：<el-tag size="mini">{{ userConfigInfo.selectedBranch }}</el-tag>
    </span>
    <span class="info-item"
          v-if="userConfigInfo.selectedDir"
    >
      目录：<el-tag size="mini">{{ userConfigInfo.selectedDir }}</el-tag>
    </span>
  </div>
</template>

<script lang="ts">
import {defineComponent, computed, reactive, toRefs} from 'vue'
import {UserConfigInfoModel} from '../common/model/userConfigInfo.model'
import {useStore} from 'vuex'

export default defineComponent({
  name: 'selected-info-bar',

  setup() {
    const store = useStore()

    const reactiveData = reactive({
      userConfigInfo: computed((): UserConfigInfoModel => store.getters.getUserConfigInfo),
    })

    return {
      ...toRefs(reactiveData),
    }
  }

})
</script>

<style scoped lang="stylus">

.selected-info-bar-box {
  height 100%
  display flex
  align-items center
  justify-content flex-start
  font-size 12px
  box-sizing border-box

  .info-item {
    margin-right 8px

    &:last-child {
      margin-right 0
    }
  }
}

</style>
