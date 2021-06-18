<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div>
    <ConfigProvider :locale="antdLocale">
      <DatePicker v-model:value="dateValue"></DatePicker>
    </ConfigProvider>
  </div>
  <div>当前语言：{{ localeLabel }}</div>
  <div><button @click="toggleLocale">切换语言</button></div>
</template>

<script>
import { ConfigProvider, DatePicker } from "ant-design-vue";
import zhAntdLocale from "ant-design-vue/es/locale/zh_CN";
import enAntdLocale from "ant-design-vue/es/locale/en_US";
import { computed, ref } from "vue";
export default {
  name: "App",
  components: {
    ConfigProvider,
    DatePicker,
  },
  setup() {
    const dateValue = ref();
    const curLocale = ref("en");
    const antdLocale = computed(() => {
      return curLocale.value === "zh" ? zhAntdLocale : enAntdLocale;
    });
    const localeLabel = computed(() => {
      return curLocale.value === "zh" ? "中文" : "英文";
    });
    const toggleLocale = () => {
      if (curLocale.value === "zh") {
        curLocale.value = "en";
      } else {
        curLocale.value = "zh";
      }
    };
    return {
      localeLabel,
      antdLocale,
      dateValue,
      toggleLocale,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
