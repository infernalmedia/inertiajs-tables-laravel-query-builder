<template>
  <ButtonWithDropdown
    class="table-filter"
    :class="hasEnabledFilter ? 'table-filter--active' : null"
    :active="hasEnabledFilter"
    placement="bottom-end"
  >
    <template #button>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          fill-rule="evenodd"
          d="M3 3a1 1 0 011-1h12a1 1 0 011 1v3a1 1 0 01-.293.707L12 11.414V15a1 1 0 01-.293.707l-2 2A1 1 0 018 17v-5.586L3.293 6.707A1 1 0 013 6V3z"
          clip-rule="evenodd"
        />
      </svg>
    </template>

    <div
      role="menu"
      class="table-filter__menu"
      aria-orientation="vertical"
      aria-labelledby="sort-menu"
    >
      <div v-for="filter in filters" :key="filter.key">
        <h3>
          {{ filter.label }}
        </h3>
        <div class="select-container">
          <select
            :value="filter.value"
            @change="onChange(filter.key, $event.target.value)"
          >
            <option
              v-for="(option, key) in filter.options"
              :value="key"
              :key="key"
            >
              {{ option }}
            </option>
          </select>
        </div>
      </div>
    </div>
  </ButtonWithDropdown>
</template>

<script>
import ButtonWithDropdown from "./ButtonWithDropdown.vue";
import TableFilter from "./../Components/TableFilter.vue";

export default {
  mixins: [TableFilter],

  components: {
    ButtonWithDropdown,
  },
};
</script>
<style>
.table-filter svg {
  height: 1.25rem;
  width: 1.25rem;
  color: rgba(156, 163, 175, var(--dt-text-opacity));
}
.table-filter--active svg {
  color: rgba(52, 211, 153, var(--dt-text-opacity));
}

.table-filter__menu h3 {
  text-transform: uppercase;
  background-color: rgba(243, 244, 246, var(--dt-bg-opacity));
  letter-spacing: 0.025em;
  line-height: 1rem;
  font-size: 0.8rem;
  padding: 1rem;
  margin: 0;
}
.table-filter__menu .select-container {
  padding: 0.5rem;
}
.table-filter__menu .select-container select {
  display: block;
  width: 100%;
  border-color: rgb(209 213 219 / var(--dt-border-opacity));
  border-radius: 0.375rem;
  box-shadow: 0 0.125rem 0.25rem rgba(24, 24, 24, 0.075);
}
.table-filter__menu .select-container select::focus {
  outline: 2px solid transparent;
  outline-offset: 2px;
  --dt-ring-opacity: 1;
  --dt-ring-inset: var(--dt-empty);
  --dt-ring-offset-width: 0px;
  --dt-ring-offset-color: #fff;
  --dt-ring-color: rgba(
    var(--dt-border-color, 99, 102, 241) var(--dt-ring-opacity)
  );
  --dt-ring-offset-shadow: var(--dt-ring-inset) 0 0 0
    var(--dt-ring-offset-width) var(--dt-ring-offset-color);
  --dt-ring-shadow: var(--dt-ring-inset) 0 0 0
    calc(1px + var(--dt-ring-offset-width)) var(--dt-ring-color);
  box-shadow: var(--dt-ring-offset-shadow), var(--dt-ring-shadow),
    var(--dt-shadow);
  border-color: rgba(
    var(--dt-input-border-color, 99, 102, 241),
    var(--dt-border-opacity)
  );
  /* shadow-sm
              sm:text-sm
              border-gray-300
              rounded-md  */
}
@media (min-width: 640px) .table-filter__menu .select-container select {
  font-size: 0.875rem;
  line-height: 1.25rem;
}
</style>
