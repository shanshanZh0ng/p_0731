<template>
    <div class="environment">
      <div class="margBot15 pad_t10">
        <i class="el-icon-s-management baseBlue"></i>
        <span>{{title}}</span>
      </div>
        <Card :cardName="cardName" :handleBtn="handleBtn" :nameIndex="$attrs.nameIndex">
          <EnvTabContent></EnvTabContent>
        </Card>
    </div>
</template>

<script>
import Card from '@/components/card'
import EnvTabContent from './envTabContent'

export default {
  name: 'Environment',
  data () {
    return {
      title: '环境设置',
      cardName: 'environment',
      handleBtn: false
    }
  },
  mounted () {
  },
  methods: {
  },

  components: {
    Card,
    EnvTabContent
  }
}
</script>

<style scoped>
</style>
