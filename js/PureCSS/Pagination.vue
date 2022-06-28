<template>
  <nav
    v-if="hasPagination"
    class="pagination-container"
    aria-label="pagination"
  >
    <p v-if="pagination.total < 1">{{ translations.no_results_found }}</p>
    <div v-if="pagination.total > 0" class="pagination pagination--mobile">
      <component
        :is="previousPageUrl ? 'inertia-link' : 'div'"
        :href="previousPageUrl"
        class="pagination-button"
        :class="previousPageUrl ? 'pagination-button--previous' : null"
      >
        {{ translations.previous }}
      </component>
      <component
        :is="nextPageUrl ? 'inertia-link' : 'div'"
        :href="nextPageUrl"
        class="pagination-button"
        :class="nextPageUrl ? 'pagination-button--next' : null"
      >
        {{ translations.next }}
      </component>
    </div>
    <div v-if="pagination.total > 0" class="pagination pagination--desktop">
      <div class="pagination__count">
        <div>
          <span>{{ pagination.from }}</span>
          {{ translations.to }}
          <span>{{ pagination.to }}</span>
          {{ translations.of }}
          <span>{{ pagination.total }}</span>
          {{ translations.results }}
        </div>
      </div>
      <div class="pagination__links">
        <nav
          class="relative z-0 inline-flex rounded-md shadow-sm -space-x-px"
          aria-label="Pagination"
        >
          <component
            :is="previousPageUrl ? 'inertia-link' : 'div'"
            :href="previousPageUrl"
            class="pagination-button pagination-button--previous"
          >
            <span class="sr-only">{{ translations.previous }}</span>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z"
                clip-rule="evenodd"
              />
            </svg>
          </component>

          <div v-for="(link, key) in pagination.links" :key="key">
            <slot name="link">
              <component
                v-if="!isNaN(link.label) || link.label === '...'"
                :is="link.url ? 'inertia-link' : 'div'"
                :href="link.url"
                class="pagination-button"
                :class="{
                  'hover:bg-gray-50': link.url,
                  'bg-gray-100': link.active,
                }"
              >
                {{ link.label }}
              </component>
            </slot>
          </div>

          <component
            :is="nextPageUrl ? 'inertia-link' : 'div'"
            :href="nextPageUrl"
            class="pagination-button pagination-button--next"
          >
            <span class="sr-only">{{ translations.next }}</span>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                clip-rule="evenodd"
              />
            </svg>
          </component>
        </nav>
      </div>
    </div>
  </nav>
</template>

<script>
import Pagination from "./../Components/Pagination.vue";

export default {
  mixins: [Pagination],
};
</script>
<style>
.pagination-container {
  background-color: #fff;
  padding: 0.75rem 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-top-style: solid;
  border-top-width: 1px;
  border-top-color: rgba(229, 231, 235, var(--dt-border-opacity));
}
@media (min-width: 640px) {
  .pagination-container {
    padding: 0.75rem 1.5rem;
  }
}
.pagination {
  /* hidden sm:flex-1 sm:flex sm:items-center sm:justify-between */
  display: flex;
  flex: 1 1 0%;
  align-items: center;
  justify-content: space-between;
}
.pagination__count {
  display: none;
}
.pagination__links > nav {
  position: relative;
  display: inline-flex;
  z-index: 0;
  border-radius: 0.375rem;
  --dt-space-x-reverse: 0;
  margin-right: calc(-1px * var(--dt-space-x-reverse));
  margin-left: calc(-1px * calc(1 - var(--dt-space-x-reverse)));
  box-shadow: 0 0.125rem 0.25rem rgba(24, 24, 24, 0.075);
  /* relative z-0 inline-flex rounded-md shadow-sm -space-x-px */
}
@media (min-width: 640px) {
  .pagination--mobile {
    display: none;
  }
}
@media (max-width: 639.98px) {
  .pagination--desktop {
    display: none;
  }
}
@media (min-width: 1024px) {
  .pagination__count > div {
    display: block;
    font-size: 0.7rem;
    color: rgba(55, 65, 81, var(--dt-text-opacity));
  }
  .pagination__count span {
    font-weight: 700;
  }
}

.pagination-button {
  position: relative;
  display: inline-flex;
  align-items: center;
  padding: 0.5rem 1rem;
  border: 1px solid #dee2e6;
  font-weight: 500;
  font-size: 0.7rem;
  color: rgb(107 114 128 / var(--dt-text-opacity));
  background-color: #fff;
  border-radius: 0;
  min-height: 100%;
}

@media (max-width: 639.98px) {
  .pagination-button {
    border-radius: 0.375rem;
  }
}
.pagination-button:hover {
  color: rgba(55, 65, 81, var(--dt-text-opacity));
  cursor: pointer;
}
.pagination-button svg {
  height: 1.25rem;
  width: 1.25rem;
}
.pagination-button--previous {
  border-top-left-radius: 0.375rem;
  border-bottom-left-radius: 0.375rem;
}
.pagination-button--next {
  border-top-right-radius: 0.375rem;
  border-bottom-right-radius: 0.375rem;
}
@media (max-width: 639.98px) {
  .pagination-button--next {
    margin-left: 0.75rem;
  }
}
</style>
