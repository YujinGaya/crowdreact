<template>
  <div>
    <div class="navigation-bar">
      <div class="menu is-left">
        <router-link :to="{
          name: 'emotion',
          params: {
            name: $route.params.name
          }
        }">
          <i class="fas fa-chevron-circle-left"></i>
          {{ $route.params.name }}
        </router-link>
      </div>
      <div class="menu is-right">
        <!-- <i class="fas fa-share-alt"></i> -->
      </div>
    </div>
    <div class="graph-container">
      <!-- <MiddleLine/> -->
      <Graph/>
      <GraphCommentList/>
      <GraphEmotionButtons/>
    </div>
  </div>
</template>

<script>
import Graph from '@/components/Graph.vue'
import GraphCommentList from '@/components/GraphCommentList.vue'
import GraphEmotionButtons from '@/components/GraphEmotionButtons.vue'
// import MiddleLine from '@/components/MiddleLine.vue'

export default {
  components: {
    Graph, GraphCommentList, GraphEmotionButtons
    // , MiddleLine
  }
}
</script>

<style scoped>
.navigation-bar {
  background-color: var(--theme-blue);
  padding: 0.75rem;
  display: flex;
  justify-content: space-between;
}

.graph-container {
  height: calc(100vh - 48px);
}
</style>
