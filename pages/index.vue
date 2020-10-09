<template>
  <section class="home">
    <div class="container">
      <home-search />
      <home-content />
    </div>
  </section>
</template>

<script>
import HomeSearch from "~/components/Home/HomeSearch";
import HomeContent from "~/components/Home/HomeContent";
export default {
  components: {HomeContent, HomeSearch}
}
</script>
