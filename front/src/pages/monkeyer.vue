<template>
  <eb-page>
    <eb-navbar large largeTransparent :title="$text('Monkey Test')" eb-back-link="Back"> </eb-navbar>
    <f7-block strong>
      <div class="alert-info">{{$text('MonkeyerTestTip1')}}</div>
      <template v-if="moduleTestParty">
        <monkeyeeComponent></monkeyeeComponent>
      </template>
    </f7-block>
  </eb-page>
</template>
<script>
export default {
  data() {
    return {
      moduleTestParty: null,
    };
  },
  created() {
    // monkey route
    console.log('monkey-route module:', this.$module.name);
    // monkey store: getters
    const message2 = this.$store.getters['test/party/message2'];
    console.log('monkey-store message2:', message2);
    // monkey store: mutations
    const messageOld = this.$store.getState('test/party/message');
    this.$store.commit('test/party/setMessage', 'test for monkey');
    const messageNew = this.$store.getState('test/party/message');
    console.log('monkey-store setMessage:', messageNew);
    this.$store.commit('test/party/setMessage', messageOld);
    // monkey config
    console.log('monkey-config monkeyed:', this.$meta.config.modules['test-party'].monkeyed);
    // monkey component
    this.$meta.module.use('test-party', module => {
      this.$options.components.monkeyeeComponent = module.options.components.monkeyeeComponent;
      this.moduleTestParty = module;
    });
  },
};

</script>
<style scoped>
</style>
