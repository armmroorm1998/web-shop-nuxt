<template>
  <div class="bg-white">
    <div>
      <div class="relative z-40 lg:hidden" role="dialog" aria-modal="true" v-show="isModal">
        <div class="fixed inset-0 bg-black bg-opacity-25"></div>
        <div class="fixed inset-0 flex z-40">
          <div
            class="ml-auto relative max-w-xs w-full h-full bg-white shadow-xl py-4 pb-12 flex flex-col overflow-y-auto"
          >
            <div class="px-4 flex items-center justify-between">
              <h2 class="text-lg font-medium text-gray-900">Filters</h2>
              <button
                type="button"
                class="-mr-2 w-10 h-10 bg-white p-2 rounded-md flex items-center justify-center text-gray-400"
                @click="isModal = !isModal"
              >
                <span class="sr-only">Close menu</span>
                <!-- Heroicon name: outline/x -->
                <svg
                  class="h-6 w-6"
                  xmlns="http://www.w3.org/2000/svg"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke-width="2"
                  stroke="currentColor"
                  aria-hidden="true"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M6 18L18 6M6 6l12 12"
                  />
                </svg>
              </button>
            </div>

            <!-- Filters -->
            <form class="mt-4 border-t border-gray-200">
              <div class="border-t border-gray-200 px-4 py-6">
                <h3 class="-mx-2 -my-3 flow-root">
                  <!-- Expand/collapse section button -->
                  <button
                    type="button"
                    class="px-2 py-3 bg-white w-full flex items-center justify-between text-gray-400 hover:text-gray-500"
                    aria-controls="filter-section-mobile-0"
                    aria-expanded="false"
                    @click="toggleColor"
                  >
                    <span class="font-medium text-gray-900"> Color </span>
                  </button>
                </h3>
                <!-- Filter section, show/hide based on section state. -->
                <div class="pt-6" id="filter-section-mobile-0" v-show="isColor">
                  <div class="space-y-6">
                    <div class="flex items-center" v-for="color in colors">
                      <input
                        :id="`filter-color-${color.title}`"
                        :name="color.title"
                        :value="color.title"
                        type="checkbox"
                        class="h-4 w-4 border-gray-300 rounded text-indigo-600 focus:ring-indigo-500"
                      />
                      <label
                        :for="`filter-color-${color.title}`"
                        class="ml-3 text-sm text-gray-600"
                      >
                        {{ color.title }}
                      </label>
                    </div>
                  </div>
                </div>
              </div>

              <div class="border-t border-gray-200 px-4 py-6">
                <h3 class="-mx-2 -my-3 flow-root">
                  <!-- Expand/collapse section button -->
                  <button
                    type="button"
                    class="px-2 py-3 bg-white w-full flex items-center justify-between text-gray-400 hover:text-gray-500"
                    aria-controls="filter-section-mobile-1"
                    aria-expanded="false"
                    @click="toggleCategory"
                  >
                    <span class="font-medium text-gray-900"> Category </span>
                  </button>
                </h3>
                <!-- Filter section, show/hide based on section state. -->
                <div
                  class="pt-6"
                  id="filter-section-mobile-1"
                  v-show="isCategory"
                >
                  <div class="space-y-6">
                    <div class="space-y-4">
                      <div
                        class="flex items-center"
                        v-for="category in categories"
                      >
                        <input
                          :id="`filter-category-${category.title}`"
                          :name="category.title"
                          :value="category.title"
                          type="checkbox"
                          class="h-4 w-4 border-gray-300 rounded text-indigo-600 focus:ring-indigo-500"
                        />
                        <label
                          :for="`filter-category-${category.title}`"
                          class="ml-3 text-sm text-gray-600"
                        >
                          {{ category.title }}
                        </label>
                      </div>
                    </div>
                  </div>
                </div>
              </div>

              <div class="border-t border-gray-200 px-4 py-6">
                <h3 class="-mx-2 -my-3 flow-root">
                  <!-- Expand/collapse section button -->
                  <button
                    type="button"
                    class="px-2 py-3 bg-white w-full flex items-center justify-between text-gray-400 hover:text-gray-500"
                    aria-controls="filter-section-mobile-2"
                    aria-expanded="false"
                    @click="toggleSize"
                  >
                    <span class="font-medium text-gray-900"> Size </span>
                  </button>
                </h3>
                <!-- Filter section, show/hide based on section state. -->
                <div class="pt-6" id="filter-section-mobile-2" v-show="isSize">
                  <div class="space-y-6">
                    <div class="flex items-center" v-for="size in sizes">
                      <input
                        :id="`filter-size-${size.title}`"
                        :name="size.title"
                        :value="size.title"
                        type="checkbox"
                        class="h-4 w-4 border-gray-300 rounded text-indigo-600 focus:ring-indigo-500"
                      />
                      <label
                        :for="`filter-size-${size.title}`"
                        class="ml-3 text-sm text-gray-600"
                      >
                        {{ size.title }}
                      </label>
                    </div>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>

      <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div
          class="relative z-10 flex items-baseline justify-between pt-24 pb-6 border-b border-gray-200"
        >
          <h1 class="text-4xl font-extrabold tracking-tight text-gray-900">
            New Arrivals
          </h1>

          <div class="flex items-center">
            <div class="relative inline-block text-left">
              <div>
                <button
                  type="button"
                  class="group inline-flex justify-center text-sm font-medium text-gray-700 hover:text-gray-900"
                  id="menu-button"
                  aria-expanded="false"
                  aria-haspopup="true"
                  @click="toggleSort()"
                >
                  Sort
                  <!-- Heroicon name: solid/chevron-down -->
                  <svg
                    class="flex-shrink-0 -mr-1 ml-1 h-5 w-5 text-gray-400 group-hover:text-gray-500"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                    aria-hidden="true"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                      clip-rule="evenodd"
                    />
                  </svg>
                </button>
              </div>

              <transition
                enter-active-class="transition ease-out duration-100"
                enter-class="transform opacity-0 scale-95"
                enter-to-class="transform opacity-100 scale-100"
                leave-active-class="transition ease-in duration-75"
                leave-class="transform opacity-100 scale-100"
                leave-to-class="transform opacity-0 scale-95"
              >
                <div
                  v-show="isSort"
                  class="origin-top-right absolute right-0 mt-2 w-40 rounded-md shadow-2xl bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
                  role="menu"
                  aria-orientation="vertical"
                  aria-labelledby="menu-button"
                  tabindex="-1"
                >
                  <div class="py-1" role="none">
                    <a
                      v-for="sort in sorts"
                      href="#"
                      class="text-gray-500 block px-4 py-2 text-sm hover:bg-gray-100 focus:bg-gray-100 focus:font-medium focus:text-gray-900"
                      role="menuitem"
                      tabindex="-1"
                      id="menu-item-0"
                    >
                      {{ sort.title }}
                    </a>
                  </div>
                </div>
              </transition>
            </div>

            <button
              type="button"
              class="p-2 -m-2 ml-5 sm:ml-7 text-gray-400 hover:text-gray-500"
            >
              <span class="sr-only">View grid</span>
              <!-- Heroicon name: solid/view-grid -->
              <svg
                class="w-5 h-5"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  d="M5 3a2 2 0 00-2 2v2a2 2 0 002 2h2a2 2 0 002-2V5a2 2 0 00-2-2H5zM5 11a2 2 0 00-2 2v2a2 2 0 002 2h2a2 2 0 002-2v-2a2 2 0 00-2-2H5zM11 5a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V5zM11 13a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"
                />
              </svg>
            </button>
            <button
              type="button"
              class="p-2 -m-2 ml-4 sm:ml-6 text-gray-400 hover:text-gray-500 lg:hidden"
              @click="isModal = !isModal"
            >
              <span class="sr-only">Filters</span>
              <!-- Heroicon name: solid/filter -->
              <svg
                class="w-5 h-5"
                aria-hidden="true"
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
            </button>
          </div>
        </div>

        <section aria-labelledby="products-heading" class="pt-6 pb-24">
          <h2 id="products-heading" class="sr-only">Products</h2>

          <div class="grid grid-cols-1 lg:grid-cols-4 gap-x-8 gap-y-10">
            <!-- Filters -->
            <form class="hidden lg:block">
              <div class="border-b border-gray-200 py-6">
                <h3 class="-my-3 flow-root">
                  <!-- Expand/collapse section button -->
                  <button
                    type="button"
                    class="py-3 bg-white w-full flex items-center justify-between text-sm text-gray-400 hover:text-gray-500"
                    aria-controls="filter-section-0"
                    aria-expanded="false"
                    @click="toggleColor"
                  >
                    <span class="font-medium text-gray-900"> Color </span>
                  </button>
                </h3>

                <!-- Filter section, show/hide based on section state. -->
                <div class="pt-6" id="filter-section-0" v-show="isColor">
                  <div class="space-y-4">
                    <div class="flex items-center" v-for="color in colors">
                      <input
                        :id="`filter-color-${color.title}`"
                        :name="color.title"
                        :value="color.title"
                        type="checkbox"
                        class="h-4 w-4 border-gray-300 rounded text-indigo-600 focus:ring-indigo-500"
                      />
                      <label
                        :for="`filter-colors-${color.title}`"
                        class="ml-3 text-sm text-gray-600"
                      >
                        {{ color.title }}
                      </label>
                    </div>
                  </div>
                </div>
              </div>

              <div class="border-b border-gray-200 py-6">
                <h3 class="-my-3 flow-root">
                  <!-- Expand/collapse section button -->
                  <button
                    type="button"
                    class="py-3 bg-white w-full flex items-center justify-between text-sm text-gray-400 hover:text-gray-500"
                    aria-controls="filter-section-1"
                    aria-expanded="false"
                    @click="toggleCategory"
                  >
                    <span class="font-medium text-gray-900"> Category </span>
                  </button>
                </h3>
                <!-- Filter section, show/hide based on section state. -->
                <div class="pt-6" id="filter-section-1" v-show="isCategory">
                  <div class="space-y-4">
                    <div
                      class="flex items-center"
                      v-for="category in categories"
                    >
                      <input
                        :id="`filter-category-${category.title}`"
                        :name="category.title"
                        :value="category.title"
                        type="checkbox"
                        class="h-4 w-4 border-gray-300 rounded text-indigo-600 focus:ring-indigo-500"
                      />
                      <label
                        :for="`filter-category-${category.title}`"
                        class="ml-3 text-sm text-gray-600"
                      >
                        {{ category.title }}
                      </label>
                    </div>
                  </div>
                </div>
              </div>

              <div class="border-b border-gray-200 py-6">
                <h3 class="-my-3 flow-root">
                  <!-- Expand/collapse section button -->
                  <button
                    type="button"
                    class="py-3 bg-white w-full flex items-center justify-between text-sm text-gray-400 hover:text-gray-500"
                    aria-controls="filter-section-2"
                    aria-expanded="false"
                    @click="toggleSize"
                  >
                    <span class="font-medium text-gray-900"> Size </span>
                  </button>
                </h3>
                <!-- Filter section, show/hide based on section state. -->
                <div class="pt-6" id="filter-section-2" v-show="isSize">
                  <div class="space-y-4">
                    <div class="flex items-center" v-for="size in sizes">
                      <input
                        :id="`filter-size-${size.title}`"
                        :name="size.title"
                        :value="size.title"
                        type="checkbox"
                        class="h-4 w-4 border-gray-300 rounded text-indigo-600 focus:ring-indigo-500"
                      />
                      <label
                        :for="`filter-size-${size.title}`"
                        class="ml-3 text-sm text-gray-600"
                      >
                        {{ size.title }}
                      </label>
                    </div>
                  </div>
                </div>
              </div>
            </form>

            <!-- Product grid -->
            <div class="lg:col-span-3">
              <!-- Replace with your content -->
              <ProductList />
              <!-- /End replace -->
            </div>
          </div>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductCategories",
  data() {
    return {
      isSort: false,
      isColor: true,
      isCategory: true,
      isSize: true,
      isModal: false,
      sorts: [
        { title: "Most Popular" },
        { title: "Best Rating" },
        { title: "Newest" },
        { title: "Price: Low to High" },
        { title: "Price: High to Low" },
      ],
      colors: [
        { title: "White" },
        { title: "Beige" },
        { title: "Blue" },
        { title: "Brown" },
        { title: "Green" },
        { title: "Purple" },
      ],
      categories: [
        { title: "New Arrivals" },
        { title: "Sale" },
        { title: "Travel" },
        { title: "Organization" },
        { title: "Accessories" },
      ],
      sizes: [
        { title: "S" },
        { title: "M" },
        { title: "L" },
        { title: "XL" },
        { title: "2XL" },
      ],
    };
  },
  methods: {
    toggleSort() {
      this.isSort = !this.isSort;
    },
    toggleColor() {
      this.isColor = !this.isColor;
    },
    toggleCategory() {
      this.isCategory = !this.isCategory;
    },
    toggleSize() {
      this.isSize = !this.isSize;
    },
  },
};
</script>

<style scoped></style>
