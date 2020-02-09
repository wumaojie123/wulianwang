<template>
<div class="main">
  <cell label="更改登录密码" value=" " arrow label-color="#333" @click.native="goSetPassword"/>
  <cell v-if="isApprove" label="注销账号" value=" " arrow label-color="#333" @click.native="goAccountCancellation">
    <div slot="bottom" class="desc">操作后信息不可恢复，请谨慎考虑</div>
  </cell>
  <div class="sd">666</div>
  <div>555</div>
  <div class="sd">888</div>
  <span>hahaha</span>
  <p>157623</p>
</div>
</template>

<script>
import Cell from '@/components/lyy-cell';
import { getIsMainAccountStatus } from '../../apis/marketing/marketing';

export default {
  name: 'accountSecurity',
  components: {
    Cell,
  },
  data() {
    return {
      isApprove: false,
    };
  },
  mounted() {
    this.setApprove();
  },
  methods: {
    goSetPassword() {
      window.location.href = '/group/password-confirm.html';
    },

    /**
     * @description: 只有主账号拥有权限
     */
    async setApprove() {
      const res = await getIsMainAccountStatus();
      if (res.data) {
        this.isApprove = res.data;
      }
    },
    goAccountCancellation() {
      this.$router.push({
        path: '/accountCancellationValidator',
      });
    },
  },
};
</script>

<style lang="less" scoped>
.main{
  .lyyCell{
    &:not(:first-child){
      margin-top: 0.03rem;
    }
    .desc{
      height:0.29rem;
      font-size:0.24rem;
      font-weight:400;
      color:rgba(153,153,153,1);
      line-height:0.29rem;
      margin-top: -0.2rem;
    }
  }
}
</style>
