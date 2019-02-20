<template>
  <div>
    <div class="main-form"><ticket></ticket></div>
  </div>
</template>

<script>
import Ticket from "./Ticket";
import FilterBar from "./FilterBar";

export default {
  components: {
    ticket: Ticket,
    "filter-bar": FilterBar
  }
};
</script>

<style lang="scss" src="../styles/body/main-form.scss"></style>
