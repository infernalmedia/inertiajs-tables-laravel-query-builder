<template>
  <ButtonWithDropdown
    class="table-add-search-row"
    ref="dropdown"
    v-if="hasRows"
    :disabled="!rowsLeft"
  >
    <template #button>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M12 9v3m0 0v3m0-3h3m-3 0H9m12 0a9 9 0 11-18 0 9 9 0 0118 0z"
        />
      </svg>
      <span>{{ translations.filter }}</span>
    </template>

    <div
      class="table-add-search-row__menu"
      role="menu"
      aria-orientation="vertical"
      aria-labelledby="sort-menu"
    >
      <div
        role="menu"
        aria-orientation="vertical"
        aria-labelledby="options-menu"
      >
        <button
          v-for="searchOption in rows"
          v-show="showRow(searchOption)"
          :key="searchOption.key"
          @click.prevent="enableSearch(searchOption.key)"
          role="menuitem"
        >
          {{ searchOption.label }}
        </button>
      </div>
    </div>
  </ButtonWithDropdown>
</template>

<script>
import ButtonWithDropdown from "./ButtonWithDropdown.vue";
import OnClickOutside from "./../Components/OnClickOutside.vue";
import TableAddSearchRow from "./../Components/TableAddSearchRow.vue";

export default {
  mixins: [TableAddSearchRow],

  components: {
    ButtonWithDropdown,
    OnClickOutside,
  },
};
</script>
<style>
.table-add-search-row {
  width: auto;
}
.table-add-search-row svg {
  height: 1.25rem;
  width: 1.25rem;
  margin-right: 0.5rem;
  color: rgba(var(--dt-text-color, 156, 163, 175), var(--dt-text-opacity));
}
.table-add-search-row__menu > div {
  padding: 0.5rem 0;
}
.table-add-search-row__menu button {
  width: 100%;
  text-align: left;
  padding: 1rem 0.5rem;
  font-size: 0.875rem;
  line-height: 1.25rem;
  color: rgba(var(--dt-text-color, 55, 65, 81), var(--dt-text-opacity));
  border-width: 0;
  background-color: transparent;
}
.table-add-search-row__menu button:hover {
  background-color: rgba(
    var(--dt-bg-color, 243, 244, 246),
    var(--dt-bg-opacity)
  );
  color: rgba(17, 24, 39, var(--tw-text-opacity));
  /* hover:bg-gray-100 hover:text-gray-900 */
}
</style>
