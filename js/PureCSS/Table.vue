<template>
  <div>
    <div class="table-filters">
      <slot
        name="tableFilter"
        :hasFilters="hasFilters"
        :filters="filters"
        :changeFilterValue="changeFilterValue"
      >
        <TableFilter
          v-if="hasFilters"
          :filters="filters"
          :on-change="changeFilterValue"
        />
      </slot>

      <slot
        name="tableGlobalSearch"
        :search="search"
        :changeGlobalSearchValue="changeGlobalSearchValue"
      >
        <div class="table-global-search">
          <TableGlobalSearch
            v-if="search && search.global"
            :value="search.global.value"
            :on-change="changeGlobalSearchValue"
          />
        </div>
      </slot>

      <slot
        name="tableAddSearchRow"
        :hasSearchRows="hasSearchRows"
        :search="search"
        :newSearch="newSearch"
        :enableSearch="enableSearch"
      >
        <TableAddSearchRow
          v-if="hasSearchRows"
          :rows="search"
          :new="newSearch"
          :on-add="enableSearch"
        />
      </slot>

      <slot
        name="tableColumns"
        :hasColumns="hasColumns"
        :columns="columns"
        :changeColumnStatus="changeColumnStatus"
      >
        <TableColumns
          v-if="hasColumns"
          :columns="columns"
          :on-change="changeColumnStatus"
        />
      </slot>
    </div>

    <slot
      name="tableSearchRows"
      :hasSearchRows="hasSearchRows"
      :search="search"
      :newSearch="newSearch"
      :disableSearch="disableSearch"
      :changeSearchValue="changeSearchValue"
    >
      <TableSearchRows
        ref="rows"
        v-if="hasSearchRows"
        :rows="search"
        :new="newSearch"
        :on-remove="disableSearch"
        :on-change="changeSearchValue"
      />
    </slot>

    <slot name="tableWrapper" :meta="meta">
      <TableWrapper
        class="table-wrapper"
        :class="{ 'table-wrapper--not-only-data': !onlyData }"
      >
        <slot name="table">
          <table>
            <thead>
              <slot name="head" />
            </thead>

            <tbody>
              <slot name="body" />
            </tbody>
          </table>
        </slot>

        <slot name="pagination">
          <Pagination :meta="paginationMeta" />
        </slot>
      </TableWrapper>
    </slot>
  </div>
</template>

<script>
import Pagination from "./Pagination.vue";
import Table from "./../Components/Table.vue";
import TableAddSearchRow from "./TableAddSearchRow.vue";
import TableColumns from "./TableColumns.vue";
import TableFilter from "./TableFilter.vue";
import TableGlobalSearch from "./TableGlobalSearch.vue";
import TableSearchRows from "./TableSearchRows.vue";
import TableWrapper from "./TableWrapper.vue";

export default {
  mixins: [Table],

  components: {
    Pagination,
    TableAddSearchRow,
    TableColumns,
    TableFilter,
    TableGlobalSearch,
    TableSearchRows,
    TableWrapper,
  },
};
</script>
<style>
:root {
  --dt-text-opacity: 1;
  --dt-bg-opacity: 1;
  --dt-divide-y-reverse: 0;
  --dt-divide-opacity: 1;
  --dt-border-opacity: 1;
  --dt-input-border-color: 209, 213, 219;
}
</style>

<style scoped>
table :deep(th) {
  font-weight: 500;
  font-size: 0.75rem;
  line-height: 1rem;
  padding: 0.75rem 1.5rem;
  text-align: left;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: rgba(var(--dt-text-color, 107, 114, 128), var(--dt-text-opacity));
}

table :deep(td) {
  font-size: 0.875rem;
  line-height: 1.25rem;
  padding: 1rem 1.5rem;
  color: rgba(var(--dt-text-color, 107, 114, 128), var(--dt-text-opacity));
  white-space: nowrap;
}

table :deep(tr):hover td {
  background-color: rgba(
    var(--dt-bg-color, 249, 250, 251),
    var(--dt-bg-opacity)
  );
}

.table-filters {
  display: flex;
}
.table-filters > * + * {
  margin-left: 1rem;
}

.table-global-search {
  flex-grow: 1;
}
.table-wrapper {
}
.table-wrapper--not-only-data {
  margin-top: 0.5rem;
}
.table-wrapper table {
  min-width: 100%;
  background-color: rgba(
    var(--dt-bg-color, 255, 255, 255),
    var(--dt-bg-opacity)
  );
}

.table-wrapper table > * + * {
  border-top-width: calc(1px * calc(1 - var(--dt-divide-y-reverse)));
  border-bottom-width: calc(1px * var(--dt-divide-y-reverse));
  border-color: rgba(
    var(--dt-border-color, 229, 231, 235),
    var(--dt-divide-opacity)
  );
}

.table-wrapper table > thead {
  background-color: rgba(
    var(--dt-bg-color, 249, 250, 251),
    var(--dt-bg-opacity)
  );
}
</style>
