<template>
  <ButtonWithDropdown
    class="table-columns"
    :class="hasDisabledFilter ? 'table-columns--active' : null"
    placement="bottom-end"
    :active="hasDisabledFilter"
  >
    <template #button>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 20 20"
        fill="currentColor"
      >
        <path
          d="M10 6a2 2 0 110-4 2 2 0 010 4zM10 12a2 2 0 110-4 2 2 0 010 4zM10 18a2 2 0 110-4 2 2 0 010 4z"
        />
      </svg>
    </template>

    <div
      class="table-columns__menu"
      role="menu"
      aria-orientation="vertical"
      aria-labelledby="sort-menu"
    >
      <div>
        <ul>
          <li
            class="column-selector"
            v-for="(column, key) in columns"
            :key="key"
          >
            <p class="column-selector__label" :id="column.key">
              {{ column.label }}
            </p>

            <button
              @click.prevent="toggle(key)"
              type="button"
              class="column-selector__button"
              :class="{
                'column-selector__button--enabled': column.enabled,
                'column-selector__button--disabled': !column.enabled,
                'column-selector__button--last-item': isLastEnabledFilter(key),
              }"
              :disabled="isLastEnabledFilter(key)"
              :aria-pressed="column.enabled"
              :aria-labelledby="`option-${column.key}-label`"
              :aria-describedby="`option-${column.key}-description`"
            >
              <span class="sr-only">Use setting</span>
              <span
                aria-hidden="true"
                class="column-selector-toggle-button"
                :class="{
                  'column-selector-toggle-button--enabled': column.enabled,
                  'column-selector-toggle-button--disabled': !column.enabled,
                }"
              ></span>
            </button>
          </li>
        </ul>
      </div>
    </div>
  </ButtonWithDropdown>
</template>

<script>
import ButtonWithDropdown from "./ButtonWithDropdown.vue";
import TableColumns from "./../Components/TableColumns.vue";

export default {
  mixins: [TableColumns],

  components: {
    ButtonWithDropdown,
  },
};
</script>
<style>
.table-columns svg {
  height: 1.25rem;
  width: 1.25rem;
  color: rgba(156, 163, 175, var(--dt-text-opacity));
}
.table-columns--active svg {
  color: rgba(52, 211, 153, var(--dt-text-opacity));
}
.table-columns__menu > div {
  padding: 0.5rem 0;
}

.table-columns__menu > div > ul > * + * {
  border-top-width: calc(1px * calc(1 - var(--dt-divide-y-reverse)));
  border-bottom-width: calc(1px * var(--dt-divide-y-reverse));
  border-color: rgba(229, 231, 235, var(--dt-divide-opacity));
}
.table-columns__menu > div > ul .column-selector {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem;
}
.column-selector__label {
  color: rgba(var(--dt-text-color, 17 24 39), var(--dt-text-opacity));
  font-weight: 500;
  font-size: 0.7rem;
}
.column-selector__button {
  padding: 0;
  margin: 0 0 0 1rem;
  position: relative;
  display: inline-flex;
  flex-shrink: 0;
  height: 1.5rem;
  width: 2.75rem;
  border-width: 2px;
  border-color: transparent;
  border-radius: 9999px;
  cursor: pointer;
  transition-property: background-color, border-color, color, fill, stroke;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 200ms;
}

.column-selector__button:focus {
  outline: 2px solid transparent;
  outline-offset: 2px;
  --dt-ring-offset-width: 2px;
  --dt-ring-color: rgba(96, 165, 250, var(--dt-ring-opacity));
  box-shadow: var(--dt-ring-inset) 0 0 0 calc(2px + var(--dt-ring-offset-width))
    var(--dt-ring-color);
}
.column-selector__button--enabled {
  background-color: rgba(16, 185, 129, var(--dt-bg-opacity));
}
.column-selector__button--disabled {
  background-color: rgba(209, 213, 219, var(--dt-bg-opacity));
}
.column-selector__button--last-item {
  cursor: not-allowed;
}
.column-selector-toggle-button {
  display: inline-block;
  height: 1.25rem;
  width: 1.25rem;
  border-radius: 9999px;
  background-color: white;
  --dt-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  box-shadow: var(--dt-ring-offset-shadow, 0 0 #0000),
    var(--dt-ring-shadow, 0 0 #0000), var(--dt-shadow);
  --dt-translate-x: 0;
  transform: translateX(var(--dt-translate-x));
  box-shadow: var(--dt-ring-inset) 0 0 0
    calc(0px + var(--dt-ring-offset-width, 0px)) var(--dt-ring-color, #fff);
  transition-property: transform;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
  transition-duration: 200ms;
}
.column-selector-toggle-button--enabled {
  --dt-translate-x: 0rem;
}
.column-selector-toggle-button--disabled {
  --dt-translate-x: 1.25rem;
}
</style>
