<template>
  <el-card>
    <div>
      <div slot="header" class="clearfix">
        <h1 style="text-align: center">Login Form</h1>
      </div>

      <el-form>
        <el-form-item>
          <el-input
            v-model="username"
            placeholder="Username or email"
            prefix-icon="el-icon-user-solid"
            :disabled="loading"
          />
        </el-form-item>
        <el-form-item>
          <el-input
            v-model="password"
            placeholder="Password"
            :type="passwordVisible ? 'text' : 'password'"
            prefix-icon="el-icon-lock"
            :disabled="loading"
          >
            <i
              slot="suffix"
              :class="
                'el-input__icon ' +
                (passwordVisible ? 'el-icon-close' : 'el-icon-view')
              "
              @click="passwordVisible = !passwordVisible"
            />
          </el-input>
        </el-form-item>
        <el-row>
          <el-col :span="24" style="text-align: center">
            <el-button type="primary" :disabled="loading" @click="submit">
              Submit <i v-if="loading" class="el-icon-loading"></i
            ></el-button>
          </el-col>
        </el-row>

        <el-row :gutter="10" style="margin-top: 20px">
          <el-col :span="12"
            ><el-checkbox v-model="rememberMe"
              >Stay signed in</el-checkbox
            ></el-col
          >
          <el-col :span="12" style="text-align: right"
            ><el-link :href="passwordForgottenLink">Forgot Password</el-link></el-col
          >
        </el-row>
      </el-form>
    </div>
  </el-card>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    onsubmit: {
      type: Function,
      default() {},
    },
    passwordForgottenLink: {
      type: String,
      default: '#',
    },
  },
  data: () => ({
    username: '',
    password: '',
    rememberMe: false,
    passwordVisible: false,
    loading: false,
  }),
  methods: {
    submit() {
      this.$props.onsubmit(this.username, this.password, this.rememberMe)
    },
  },
})
</script>

<style>
</style>
