<template>
  <v-main>

    <SideBarVue />
    <div>
      <Content />
    </div>
  </v-main>
</template>

<script>
// import TopHeader from '@/components/TopHeader.vue';

import SideBarVue from '@/components/SideBar.vue';
import Content from '@/components/Content.vue';

export default {
  components: { SideBarVue, Content }

}
</script>

<style></style>
