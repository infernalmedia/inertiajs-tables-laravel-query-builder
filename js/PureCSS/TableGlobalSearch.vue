<template>
  <div class="table-global-search">
    <input
      placeholder="Search..."
      :value="value"
      type="text"
      @input="onChange($event.target.value)"
    />
    <div class="table-global-search__icon">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5 text-gray-400"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          fill-rule="evenodd"
          d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
          clip-rule="evenodd"
        />
      </svg>
    </div>
  </div>
</template>

<script>
import TableGlobalSearch from "./../Components/TableGlobalSearch.vue";

export default {
  mixins: [TableGlobalSearch],
};
</script>
<style >
.table-global-search {
  position: relative;
}
.table-global-search > input {
  display: block;
  width: 100%;
  border-color: rgb(
    var(--dt-input-border-color, 209 213 219) / var(--dt-border-opacity)
  );
  border-radius: 0.375rem;
  appearance: none;
  background-color: #fff;
  border-color: #6b7280;
  border-width: 1px;
  border-radius: 0.375rem;
  pdding: 0.5rem 0.75rem;
  color: inherit;
  margin: 0;
  font-size: 1rem;
  line-height: 1.5rem;
  font-weight: inherit;
  font-family: inherit;
  overflow: visible;
  box-shadow: 0 0.125rem 0.25rem rgba(24, 24, 24, 0.075) !important;
}
.table-global-search > input::focus {
  border-color: rgb(99 102 241 / var(--tw-border-opacity));
  outline: 2px solid transparent;
  outline-offset: 2px;
}

@media (min-width: 640px) {
  .table-global-search > input {
    font-size: 0.875rem;
    line-height: 1.25rem;
  }
}

.table-global-search > input::placeholder {
  color: #6b7280;
  opacity: 1;
}
.table-global-search__icon {
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
  padding-right: 0.75rem;
  display: flex;
  place-items: center;
  pointer-events: none;
}
</style>
