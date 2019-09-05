<template>
  <div class="home">
    <img ref="img" @click="onClick" alt="Vue logo" src="../assets/logo.png" />
    <p>{{name}}</p>
    <p>{{count}}:{{num}}</p>
    <ul>
      <li v-for="item in list" :key="item">{{item}}</li>
    </ul>
    <!-- <HelloWorld :names="name" msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import {
  reactive,
  computed,
  ref,
  toRefs,
  watch,
  onMounted
} from "@vue/composition-api";

export default {
  name: "home",
  components: {
    HelloWorld
  },
  setup() {
    const count = ref(0);
    const list = reactive([1, 2]);
    const data = reactive({
      name: "vvuuee"
    });
    const img = ref(null);

    const num = computed(() => count.value * 2);
    const stop = watch(count, (val, old) => {
      console.log("count", val);
      if (val > 5) stop();
    });
    onMounted(() => {
      console.log("onMounted");
      console.log("img", img);
    });

    function onClick() {
      count.value++;
      data.name = randomStr();
      list.push(data.name);
    }
    function randomStr() {
      return Math.random()
        .toString()
        .substring(2);
    }
    return { ...toRefs(data), list, num, count, onClick, img };
  }
};
</script>
