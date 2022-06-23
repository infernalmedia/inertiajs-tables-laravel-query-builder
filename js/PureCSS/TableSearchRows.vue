<template>
  <div class="table-search-rows" v-show="hasFiltersEnabled">
    <div class="table-search-row">
      <div class="table-search-row__label">
        <div v-for="(search, key) in enabledFilters" :key="key">
          <span>{{ search.label }}</span>
        </div>
      </div>

      <div class="table-search-row__input">
        <div
          v-for="(search, key) in enabledFilters"
          :key="key"
          class="table-search-row-input-container"
        >
          <div>
            <input
              class="table-search-row-input__field"
              :ref="search.key"
              :value="search.value"
              :placeholder="translations.placeholder"
              type="text"
              @input="onChange(search.key, $event.target.value)"
            />
            <div class="table-search-row-input__button">
              <button @click.prevent="onRemove(search.key)">
                <span class="sr-only">Remove search</span>
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
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TableSearchRows from "./../Components/TableSearchRows.vue";

export default {
  mixins: [TableSearchRows],
};
</script>
<style>
.table-search-rows {
  width: 100%;
  background-color: rgba(
    var(--dt-bg-color, 249, 250, 251),
    var(--dt-bg-opacity)
  );
  padding: 1rem;
  margin-bottom: 1rem;
  margin-top: 1rem;
  border-radius: 0.25rem;
}
.table-search-row {
  display: flex;
  flex-direction: row;
}
.table-search-row > * + * {
  --dt-space-x-reverse: 0;
  margin-right: calc(1rem * var(--dt-space-x-reverse));
  margin-left: calc(1rem * calc(1 - var(--dt-space-x-reverse)));
}
.table-search-row__label > * + * {
  --dt-space-x-reverse: 0;
  margin-right: calc(1rem * var(--dt-space-x-reverse));
  margin-left: calc(1rem * calc(1 - var(--dt-space-x-reverse)));
}
.table-search-row__label > div,
.table-search-row__input > div {
  margin: 1rem 0;
}
.table-search-row__label > div {
  height: 2rem;
  display: flex;
  align-items: center;
  justify-content: flex-end;
}
/* .table-search-row__label span {
  line-height: 1.25rem;
  font-size: 0.75%;
} */
.table-search-row__input {
  flex-grow: 1;
  --dt-space-x-reverse: 0;
  margin-right: calc(1rem * var(--dt-space-x-reverse));
  margin-left: calc(1rem * calc(1 - var(--dt-space-x-reverse)));
}
.table-search-row-input-container {
  display: flex;
  align-items: center;
  height: 2rem;
}
.table-search-row-input-container > div {
  flex-grow: 1;
  position: relative;
}
.table-search-row-input__field {
  display: block;
  width: 100%;
  border-radius: 0.375rem;
  box-shadow: 0 0.125rem 0.25rem rgba(24, 24, 24, 0.075);
  --dt-border-opacity: 1;
  border-color: rgba(209, 213, 219, var(--dt-border-opacity));
  border-style: solid;
}
.table-search-row-input__field:focus {
  border-color: rgb(99 102 241 / var(--dt-border-opacity));
  border-width: 1px;
}
@media (min-width: 640px) {
  .table-search-row-input__field {
    font-size: 0.875rem;
    line-height: 1.25rem;
  }
}

.table-search-row-input__button {
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
  padding-right: 1rem;
  display: flex;
  place-items: center;
}
.table-search-row-input__button button {
  background-color: transparent;
  border: none;
}
.table-search-row-input__button svg {
  width: 1.25rem;
  height: 1.25rem;
}
</style>
