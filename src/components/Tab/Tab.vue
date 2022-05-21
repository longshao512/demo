<template>
  <div>
    <div class="tab">
      <ul class="tab_button">
        <li
          v-for="(item, index) in tabList"
          :key="index"
          :class="{ active: currentClass == index }"
          @click="toggleTab(item.tab_con, index)"
        >
          {{ item.title }}
          <!-- 无动画效果 -->
          <!-- <div :class="{ box: currentClass == index }"></div> -->
        </li>
        <div class="box" ref="box"></div>
      </ul>
    </div>
    <div class="tab_con">
      <!-- is绑定选中tab的内容 -->
      <component :is="currentTab"></component>
    </div>
  </div>
</template>

<script>
// 引入三个tab内容组件
import firstTab from "./firstTab";
import secondTab from "./secondTab";
import thirdTab from "./thirdTab";

export default {
  name: "Home",
  props: {},
  data() {
    return {
      // 默认选中tab
      currentTab: "firstTab",
      // 默认选中按钮样式
      currentClass: 0,
      tabList: [
        {
          // tab文字
          title: "推荐",
          // tab对应内容块
          tab_con: "firstTab",
        },
        {
          title: "热门",
          tab_con: "secondTab",
        },
        {
          title: "视频",
          tab_con: "thirdTab",
        },
      ],
    };
  },
  methods: {
    toggleTab(tab_con, currentClass) {
      // 选中tab内容块展示
      this.currentTab = tab_con;
      // 选中tab样式
      this.currentClass = currentClass;
      this.$refs.box.style.transform =
        "translateX(" + 200 * this.currentClass + "px)";
      this.$refs.box.style.transition = ".5s";
    },
  },
  components: {
    firstTab,
    secondTab,
    thirdTab,
  },
};
</script>
<style scoped>
.tab {
  height: 70px;
}
.tab_button {
  display: flex;
  justify-content: space-evenly;
  padding-bottom: 20px;
}
.tab_button li {
  cursor: pointer;
  display: inline-block;
  font-size: 32px;
  color: #b3b3b3;
}
/* 选中tab 样式 */
.tab_button li.active {
  color: #2e2e2e;
  font-size: 36px;
  transition-delay: 0.2s;
}
.tab_button .box {
  width: 32px;
  height: 6px;
  background-color: #14c4bc;
  border-radius: 4px;
  position: absolute;
  top: 50px;
  left: 160px;
  cursor: pointer;
}
</style>

