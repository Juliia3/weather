<script setup>
import "./main.scss";
import Block from "../Block/Block.vue";

</script>

<template>
  <main class="main">
    <Block v-for="item in blocks" :index="item.index" :add="addBlock" />
  </main>
</template>

<script>
export default {
  data() {
    return {
      index: 0,
      blocks: [
      ],
    };
  },
  created() {
    this.blocks.push({
      index: this.index,
    });
    this.index++;
  },
  methods: {
    addBlock() {
      if (this.blocks.length < 5) {
        this.blocks.push({
          index: this.index++,
        });
      } else {
        alert("You can't add more than 5 blocks!");
      }
    },
  },
};
</script>
