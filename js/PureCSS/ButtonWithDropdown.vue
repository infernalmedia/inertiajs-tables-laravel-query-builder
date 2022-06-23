<template>
  <OnClickOutside class="button-with-dropdown-container" :do="hide">
    <div>
      <button
        @click.prevent="toggle"
        type="button"
        :disabled="disabled"
        class="button-with-dropdown__button"
        :class="{
          'button-with-dropdown__button--active': active,
          'button-with-dropdown__button--disabled': disabled,
        }"
        aria-haspopup="true"
        ref="button"
      >
        <slot name="button" />
      </button>

      <div v-show="opened" ref="tooltip" class="button-with-dropdown__dropdown">
        <div>
          <slot />
        </div>
      </div>
    </div>
  </OnClickOutside>
</template>

<script>
import ButtonWithDropdown from "./../Components/ButtonWithDropdown.vue";
import OnClickOutside from "./../Components/OnClickOutside.vue";

export default {
  mixins: [ButtonWithDropdown],

  components: {
    OnClickOutside,
  },
};
</script>
<style>
.button-with-dropdown-container > div {
  position: relative;
}
.button-with-dropdown__button {
  /* w-full bg-white border rounded-md shadow-sm px-4 py-2 inline-flex justify-center text-sm font-medium text-gray-700  */
  width: 100%;
  background-color: transparent;
  border-width: 1px;
  border-radius: 0.375rem;
  --dt-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  box-shadow: var(--dt-ring-offset-shadow, 0 0 #0000),
    var(--dt-ring-shadow, 0 0 #0000), var(--dt-shadow);
  padding: 0.5rem 1rem;
  display: inline-flex;
  justify-content: center;
  font-size: 0.875rem;
  line-height: 1.25rem;
  font-weight: 500;
  transition: background-color 0.3s ease-in-out;
  border-color: rgba(209, 213, 219, var(--dt-border-opacity));
  border-style: solid;
}
.button-with-dropdown__button--active {
  border-color: rgba(110, 231, 183, var(--dt-border-opacity));
}
.button-with-dropdown__button--disabled {
  cursor: not-allowed;
}
.button-with-dropdown__button:hover {
  background-color: rgba(107, 114, 128, var(--dt-bg-opacity));
}
.button-with-dropdown__dropdown {
  position: absolute;
  z-index: var(--dt-dropdown-index, 10);
}
.button-with-dropdown__dropdown > div {
  margin-top: 0.5rem;
  background-color: #fff;
  width: 16rem;
  border-radius: 0.375rem;
  box-shadow: 0 1rem 3rem rgba(24, 24, 24, 0.175);
}
</style>
