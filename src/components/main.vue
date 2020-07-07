<template>
  <div class="hello">
    <div class="btn__container">
      <button @click="setData">Запросить</button>
      <button @click="showData">Показать</button>
      <button @click="deleteData">Очистить</button>
    </div>
    <div class="img__container" v-if="showResult && showResult.length">
      <div
        class="img__element"
        v-for="(item, index) in showResult"
        :key="index"
      >
        <img :src="item.icon" alt="" />
        <div v-if="item.name">{{ item.name }}</div>
        <div v-if="item.description">{{ item.description }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";

Vue.use(VueAxios, axios);

export default {
  name: "MainComponent",
  data: function() {
    return {
      result: [],
      showResult: []
    };
  },
  methods: {
    async setData() {
      try {
        await this.axios
          .get("https://api.t3d.live/materials/lists")
          .then(response => {
            console.log(response);
            this.result = response.data.materialsList;
          });
      } catch (error) {
        console.log(error);
      }
    },
    showData() {
      this.showResult = this.result;
    },
    deleteData() {
      this.showResult = [];
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn__container {
  display: flex;
}
</style>
