<template>
  <th
    v-show="cell.show"
    class="header-cell"
    :class="cell.sortable ? 'header-cell--sortable' : null"
    @click.prevent="onClick"
  >
    <div class="header-cell-content">
      <slot />

      <svg
        v-if="cell.sortable"
        aria-hidden="true"
        class="column-sorting-icon"
        :class="cell.sort ? 'column-sorting-icon--sorted' : null"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 320 512"
      >
        <path
          v-if="!cell.sort"
          fill="currentColor"
          d="M41 288h238c21.4 0 32.1 25.9 17 41L177 448c-9.4 9.4-24.6 9.4-33.9 0L24 329c-15.1-15.1-4.4-41 17-41zm255-105L177 64c-9.4-9.4-24.6-9.4-33.9 0L24 183c-15.1 15.1-4.4 41 17 41h238c21.4 0 32.1-25.9 17-41z"
        />

        <path
          v-if="cell.sort === 'asc'"
          fill="currentColor"
          d="M279 224H41c-21.4 0-32.1-25.9-17-41L143 64c9.4-9.4 24.6-9.4 33.9 0l119 119c15.2 15.1 4.5 41-16.9 41z"
        />

        <path
          v-if="cell.sort === 'desc'"
          fill="currentColor"
          d="M41 288h238c21.4 0 32.1 25.9 17 41L177 448c-9.4 9.4-24.6 9.4-33.9 0L24 329c-15.1-15.1-4.4-41 17-41z"
        />
      </svg>
    </div>
  </th>
</template>

<script>
import HeaderCell from "./../Components/HeaderCell.vue";

export default {
  mixins: [HeaderCell],
};
</script>
<style >
.header-cell {
  pointer-events: none;
}
.header-cell--sortable {
  cursor: pointer;
  pointer-events: auto;
}
.header-cell-content {
  display: flex;
  flex-direction: row;
  align-items: center;
}
.column-sorting-icon {
  width: 0.75rem;
  height: 0.75rem;
  margin-left: 0.5rem;
  color: rgba(156, 163, 175, var(--dt-text-opacity));
}
.column-sorting-icon--sorted {
  color: rgba(16, 185, 129, var(--dt-text-opacity));
}
</style>
