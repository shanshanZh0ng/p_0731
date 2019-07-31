<template>
  <div class="env">
    <el-tabs v-model="name" class="inlineBlock left" style="width:100%;">
      <el-tab-pane v-for="tab in tabs" :key="tab.id" :label="tab.label" :name="tab.name">
        <el-form label-width="140px" class="demo-ruleForm" :serverData="serverData">
          <el-form-item label="选择模板/镜像" required>
            <el-radio-group v-model="serverData.server">
              <el-radio-button :label="server.server" v-for="server in serverData.tabData" :key="server.server">{{server.server}}</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="选择版本" required>
            <el-radio-group v-model="serverData.version">
              <el-radio-button :label="version.id" v-for="version in versions" :key="version.id">{{version.label}}</el-radio-button>
            </el-radio-group>
          </el-form-item>
          <el-form-item label="资源配置" required>
            <el-radio-group v-model="serverData.resource" class="left">
              <el-radio-button :label="resource.id" class="margin-r20 noradius border" v-for="resource in resources" :key="resource.id">{{resource.label}}</el-radio-button>
            </el-radio-group>
            <el-tooltip class="item" effect="dark" content="提示文字" placement="right">
              <i class="el-icon-question icon-q"></i>
            </el-tooltip>
          </el-form-item>
          <el-form-item label="子域名" required>
            <el-row class="left" style="width:80%">
              <el-col :span="18">
                <div class="center">
                  <el-input placeholder="请输入内容" v-model="serverData.domain">
                    <template slot="prepend">Http://</template>
                    <template slot="append">{{domains.first}}</template>
                  </el-input>
                </div>
              </el-col>
              <el-col class="center" :span="4">
                <div class="bg-purple-light">
                  <div class="lastInput center">{{domains.last}}</div>
                </div>
              </el-col>
              <el-col style="width: 30px;">
                <el-tooltip effect="dark" content="提示文字" placement="right">
                  <i class="el-icon-question icon-q"></i>
                </el-tooltip>
              </el-col>
            </el-row>
          </el-form-item>
        </el-form>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import {tabData} from '@/views/applicationCreator/initFormData'

export default {
  name: 'EnvTabContent',
  prop: {
    serverData: {
      type: Array,
      default: []
    }
  },
  data () {
    return {
      name: 'runningTab',
      server: '',
      versions: [],
      resources: [],
      domains: {},
      serverData: {},
      datas: tabData,
      tabs: [{name: 'runningTab', label: '公共模板', id: 1}, {name: 'mirrorTab', label: '我的镜像', id: 2}]
    }
  },
  mounted () {
    this.setEnvDefaultVal()
  },

  methods: {
    setEnvDefaultVal () {
      this.serverData = this.datas[`${this.name}`]
      const tabConten = this.serverData.tabData[0]
      this.server = tabConten.server
      this.versions = tabConten.versions
      this.resources = tabConten.resources
      this.domains = tabConten.domains
      // 设置版本和资源默认值
      this.serverData.version = this.versions[0].id
      this.serverData.resource = this.resources[0].id
    }
  },
  watch: {
    'name': function (val) {
      this.serverData = this.datas[val]
      this.versions = this.serverData.tabData[0].versions
      this.resources = this.serverData.tabData[0].resources
      this.domains = this.serverData.tabData[0].domains
      // 设置版本和资源默认值
      this.serverData.server = this.server
      this.serverData.version = this.versions[0].id
      this.serverData.resource = this.resources[0].id
    },
    'serverData.server': function (val) {
      // 设置版本和资源默认值
      this.serverData.version = this.versions[0].id
      this.serverData.resource = this.resources[0].id
    }
  }
}
</script>

<style scoped>
.lastInput {
  border: 1px solid #ccc;
  border-left:none;
  color:#909399;
  height:38px;
  line-height:38px;
  background:#F5F7FA;
}
</style>
