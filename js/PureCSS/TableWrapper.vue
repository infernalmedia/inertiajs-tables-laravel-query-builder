<template>
  <div>
    <div class="table-container">
      <div>
        <div>
          <slot />
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.table-wrapper {
  display: flex;
  flex-direction: column;
}
.table-container {
  overflow-x: auto;
  margin-top: -0.5rem;
  margin-bottom: -0.5rem;
}
@media (min-width: 640px) {
  .table-container {
    margin-left: -1.5rem;
    margin-right: -1.5rem;
  }
}
@media (min-width: 1024px) {
  .table-container {
    margin-left: -2rem;
    margin-right: -2rem;
  }
}

.table-container > div {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  min-width: 100%;
  display: inline-block;
  vertical-align: middle;
}
@media (min-width: 640px) {
  .table-container > div {
    padding-left: 1.5rem;
    padding-right: 1.5rem;
  }
}
@media (min-width: 1024px) {
  .table-container > div {
    padding-left: 2rem;
    padding-right: 2rem;
  }
}

.table-container > div > div {
  position: relative;
  box-shadow: 0 0.5rem 1rem rgba(24, 24, 24, 0.15);
  border-bottom-width: 1px;
  border-color: rgba(229 231 235, var(--dt-border-opacity));
}
</style>
