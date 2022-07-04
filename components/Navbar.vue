<template>
  <div>
    <div>
      <nav class="bg-gray-800">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex items-center justify-between h-16">
            <div class="flex items-center">
              <div class="flex-shrink-0">
                <NuxtLink to="/">
                  <img
                    class="h-8 w-8"
                    src="https://tailwindui.com/img/logos/workflow-mark-indigo-400.svg"
                    alt="Workflow logo"
                  />
                </NuxtLink>
              </div>

              <div class="hidden md:block">
                <div class="ml-10 flex items-baseline">
                  <template v-for="item in items">
                    <NuxtLink :to="item.to" class="px-4 py-2 mt-2 text-sm text-white font-semibold bg-transparent rounded-lg dark-mode:bg-transparent dark-mode:hover:bg-gray-600 dark-mode:focus:bg-gray-600 dark-mode:focus:text-white dark-mode:hover:text-white dark-mode:text-gray-200 md:mt-0 md:ml-4 hover:text-gray-900 focus:text-gray-900 hover:bg-gray-200 focus:bg-gray-200 focus:outline-none focus:shadow-outline">
                      {{ item.title }}
                    </NuxtLink>
                  </template>
                </div>
              </div>
            </div>

            <div class="hidden md:block">
              <div class="ml-4 flex items-center md:ml-6">
                <!-- Profile dropdown -->
                <div class="ml-3 relative">
                  <div>
                    <button
                      @click="toggle"
                      class="max-w-xs flex items-center text-sm rounded-full text-white focus:outline-none focus:shadow-solid"
                      id="user-menu"
                      aria-label="User menu"
                      aria-haspopup="true"
                    >
                      <img
                        class="h-8 w-8 rounded-full"
                        src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                        alt
                      />
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
                    <div v-show="isOpen" class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg">
                      <div
                        class="py-1 rounded-md bg-white shadow-xs"
                        role="menu"
                        aria-orientation="vertical"
                        aria-labelledby="user-menu"
                      >
                        <template v-for="setting in settings">
                          <NuxtLink :to="setting.to" class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100">
                            {{ setting.title }}
                          </NuxtLink>
                        </template>
                      </div>
                    </div>
                  </transition>
                </div>
              </div>
            </div>

            <div class="-mr-2 flex md:hidden">
              <!-- Mobile menu button -->
              <button @click="toggle" class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:bg-gray-700 focus:text-white">
                <svg
                  :class="[isOpen ? 'hidden' : 'block', 'h-6 w-6']"
                  stroke="currentColor"
                  fill="none"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"
                  ></path>
                </svg>
                <svg
                  :class="[isOpen ? 'block' : 'hidden', 'h-6 w-6']"
                  stroke="currentColor"
                  fill="none"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M6 18L18 6M6 6l12 12"
                  ></path>
                </svg>
              </button>
            </div>
          </div>
        </div>

        <div :class="[isOpen ? '' : 'hidden', 'md:hidden']">
          <div class="px-2 pt-2 pb-3 sm:px-3">
            <template v-for="item in items">
              <NuxtLink :to="item.to" class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-300 hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700">
                {{ item.title }}
              </NuxtLink>
            </template>
          </div>

          <div class="pt-4 pb-3 border-t border-gray-700">
            <div class="flex items-center px-5">
              <div class="flex-shrink-0">
                <img
                  class="h-10 w-10 rounded-full"
                  src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80"
                  alt
                />
              </div>
              <div class="ml-3">
                <div class="text-base font-medium leading-none text-white">
                  Tom Cook
                </div>
                <div class="mt-1 text-sm font-medium leading-none text-gray-400">
                  tom@example.com
                </div>
              </div>
            </div>
            <div class="mt-3 px-2">
              <template v-for="setting in settings">
                <NuxtLink :to="setting.to" class="block px-3 py-2 rounded-md text-base font-medium text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:text-white focus:bg-gray-700">
                  {{ setting.title }}
                </NuxtLink>
              </template>
            </div>
          </div>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      isOpen: false,
      headerTitle: "Women",
      items: [
        {
          icon: "",
          title: "Women",
          to: "/product-categories",
        },
        {
          icon: "",
          title: "Men",
          to: "/",
        },
        {
          icon: "",
          title: "Children",
          to: "/",
        },
      ],
      settings: [
        {
          title: "Your Profile",
          to: "/",
        },
        {
          title: "Setting",
          to: "/",
        },
        {
          title: "Sign Out",
          to: "/",
        },
      ],
    };
  },
  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>
