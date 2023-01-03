<template>
  <div
    v-show="show"
    class="fixed inset-0 transform transition-all"
    @click="show = false"
  />
  <div
    @click="show = !show"
    class="w-full flex items-center justify-between rounded-md border border-gray-300 bg-white dark:bg-slate-700 dark:border-sky-700 py-2 px-3 shadow-sm focus:border-sky-600 focus:outline-none focus:ring-1 focus:ring-sky-600 sm:text-sm"
  >
    <span v-if="color != ''" class="flex space-x-2 items-center">
      <div :class="[atualColor, 'w-5 h-5 rounded-sm']"></div>
      <p class="text-neutral-200">{{ color }}</p>
    </span>
    <span v-else class="flex space-x-2 items-center">
      <svg
        class="w-5 h-5"
        viewBox="0 0 24 24"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g clip-path="url(#clip0_5_124)">
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M3.51472 3.51471L12 12H0C0 8.68628 1.34315 5.68628 3.51472 3.51471Z"
            fill="#E11D48"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M3.51472 3.51472C5.68629 1.34315 8.68629 0 12 0V12L3.51472 3.51472Z"
            fill="#E99A00"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M20.4853 3.51472L12 12V0C15.3137 0 18.3137 1.34315 20.4853 3.51472Z"
            fill="#65A30D"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M20.4853 3.51471C22.6569 5.68628 24 8.68628 24 12H12L20.4853 3.51471Z"
            fill="#059669"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M20.4853 20.4853L12 12L24 12C24 15.3137 22.6569 18.3137 20.4853 20.4853Z"
            fill="#0284C7"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M20.4853 20.4853C18.3137 22.6569 15.3137 24 12 24L12 12L20.4853 20.4853Z"
            fill="#4F46E5"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M3.51472 20.4853C5.68629 22.6569 8.68629 24 12 24V12L3.51472 20.4853Z"
            fill="#9333EA"
          />
          <path
            fill-rule="evenodd"
            clip-rule="evenodd"
            d="M3.51472 20.4853C1.34315 18.3137 0 15.3137 0 12H12L3.51472 20.4853Z"
            fill="#DB2777"
          />
          <circle cx="12" cy="12" r="4" fill="#D9D9D9" />
        </g>
        <defs>
          <clipPath id="clip0_5_124">
            <rect width="24" height="24" fill="white" />
          </clipPath>
        </defs>
      </svg>
      <p class="text-neutral-200">Seletor de Cor</p>
    </span>

    <svg
      xmlns="http://www.w3.org/2000/svg"
      fill="none"
      viewBox="0 0 24 24"
      stroke-width="1.5"
      stroke="currentColor"
      class="w-5 h-5 dark:text-neutral-200"
    >
      <path
        stroke-linecap="round"
        stroke-linejoin="round"
        d="M19.5 8.25l-7.5 7.5-7.5-7.5"
      />
    </svg>
  </div>
  <div v-show="show" class="relative">
    <div
      class="absolute w-full flex justify-center top-0 right-0 p-3 rounded dark:bg-slate-700 bg-white dark:border border-sky-700 shadow"
    >
      <div
        class="flex flex-wrap justify-center w-64 h-64 overflow-auto scrollbar dark:bg-slate-700 self-center"
      >
        <span v-for="(color, index) in colorsComputed" v-bind:key="index">
          <div class="flex items-center">
            <span v-for="(column, index) in color" v-bind:key="index">
              <button
                @click="pickColor(column)"
                :class="[
                  column,
                  'w-5 h-5 hover:w-6 hover:h-6 rounded-sm flex items-center justify-center m-0.5 hover:m-0 border border-neutral-300 dark:border-neutral-800',
                ]"
              ></button>
            </span>
          </div>
        </span>
      </div>
    </div>
  </div>
  <!-- <div class="bg-red-200">Teste</div> -->
</template>

<script>
export default {
  name: "ColorPicker",
  data() {
    return {
      show: false,
    };
  },
  props: {
    color: null,
  },
  emits: ["update:color"],
  methods: {
    pickColor(color) {
      this.$emit("update:color", color.substr(3));
    },
  },
  computed: {
    atualColor() {
      return "bg-" + this.color;
    },
    colorsComputed() {
      return {
        slate: [
          "bg-slate-50",
          "bg-slate-100",
          "bg-slate-200",
          "bg-slate-300",
          "bg-slate-400",
          "bg-slate-500",
          "bg-slate-600",
          "bg-slate-700",
          "bg-slate-800",
          "bg-slate-900",
        ],
        gray: [
          "bg-gray-50",
          "bg-gray-100",
          "bg-gray-200",
          "bg-gray-300",
          "bg-gray-400",
          "bg-gray-500",
          "bg-gray-600",
          "bg-gray-700",
          "bg-gray-800",
          "bg-gray-900",
        ],
        zinc: [
          "bg-zinc-50",
          "bg-zinc-100",
          "bg-zinc-200",
          "bg-zinc-300",
          "bg-zinc-400",
          "bg-zinc-500",
          "bg-zinc-600",
          "bg-zinc-700",
          "bg-zinc-800",
          "bg-zinc-900",
        ],
        neutral: [
          "bg-neutral-50",
          "bg-neutral-100",
          "bg-neutral-200",
          "bg-neutral-300",
          "bg-neutral-400",
          "bg-neutral-500",
          "bg-neutral-600",
          "bg-neutral-700",
          "bg-neutral-800",
          "bg-neutral-900",
        ],
        stone: [
          "bg-stone-50",
          "bg-stone-100",
          "bg-stone-200",
          "bg-stone-300",
          "bg-stone-400",
          "bg-stone-500",
          "bg-stone-600",
          "bg-stone-700",
          "bg-stone-800",
          "bg-stone-900",
        ],
        red: [
          "bg-red-50",
          "bg-red-100",
          "bg-red-200",
          "bg-red-300",
          "bg-red-400",
          "bg-red-500",
          "bg-red-600",
          "bg-red-700",
          "bg-red-800",
          "bg-red-900",
        ],
        orange: [
          "bg-orange-50",
          "bg-orange-100",
          "bg-orange-200",
          "bg-orange-300",
          "bg-orange-400",
          "bg-orange-500",
          "bg-orange-600",
          "bg-orange-700",
          "bg-orange-800",
          "bg-orange-900",
        ],
        amber: [
          "bg-amber-50",
          "bg-amber-100",
          "bg-amber-200",
          "bg-amber-300",
          "bg-amber-400",
          "bg-amber-500",
          "bg-amber-600",
          "bg-amber-700",
          "bg-amber-800",
          "bg-amber-900",
        ],
        yellow: [
          "bg-yellow-50",
          "bg-yellow-100",
          "bg-yellow-200",
          "bg-yellow-300",
          "bg-yellow-400",
          "bg-yellow-500",
          "bg-yellow-600",
          "bg-yellow-700",
          "bg-yellow-800",
          "bg-yellow-900",
        ],
        lime: [
          "bg-lime-50",
          "bg-lime-100",
          "bg-lime-200",
          "bg-lime-300",
          "bg-lime-400",
          "bg-lime-500",
          "bg-lime-600",
          "bg-lime-700",
          "bg-lime-800",
          "bg-lime-900",
        ],
        green: [
          "bg-green-50",
          "bg-green-100",
          "bg-green-200",
          "bg-green-300",
          "bg-green-400",
          "bg-green-500",
          "bg-green-600",
          "bg-green-700",
          "bg-green-800",
          "bg-green-900",
        ],
        emerald: [
          "bg-emerald-50",
          "bg-emerald-100",
          "bg-emerald-200",
          "bg-emerald-300",
          "bg-emerald-400",
          "bg-emerald-500",
          "bg-emerald-600",
          "bg-emerald-700",
          "bg-emerald-800",
          "bg-emerald-900",
        ],
        teal: [
          "bg-teal-50",
          "bg-teal-100",
          "bg-teal-200",
          "bg-teal-300",
          "bg-teal-400",
          "bg-teal-500",
          "bg-teal-600",
          "bg-teal-700",
          "bg-teal-800",
          "bg-teal-900",
        ],
        cyan: [
          "bg-cyan-50",
          "bg-cyan-100",
          "bg-cyan-200",
          "bg-cyan-300",
          "bg-cyan-400",
          "bg-cyan-500",
          "bg-cyan-600",
          "bg-cyan-700",
          "bg-cyan-800",
          "bg-cyan-900",
        ],
        sky: [
          "bg-sky-50",
          "bg-sky-100",
          "bg-sky-200",
          "bg-sky-300",
          "bg-sky-400",
          "bg-sky-500",
          "bg-sky-600",
          "bg-sky-700",
          "bg-sky-800",
          "bg-sky-900",
        ],
        blue: [
          "bg-blue-50",
          "bg-blue-100",
          "bg-blue-200",
          "bg-blue-300",
          "bg-blue-400",
          "bg-blue-500",
          "bg-blue-600",
          "bg-blue-700",
          "bg-blue-800",
          "bg-blue-900",
        ],
        indigo: [
          "bg-indigo-50",
          "bg-indigo-100",
          "bg-indigo-200",
          "bg-indigo-300",
          "bg-indigo-400",
          "bg-indigo-500",
          "bg-indigo-600",
          "bg-indigo-700",
          "bg-indigo-800",
          "bg-indigo-900",
        ],
        violet: [
          "bg-violet-50",
          "bg-violet-100",
          "bg-violet-200",
          "bg-violet-300",
          "bg-violet-400",
          "bg-violet-500",
          "bg-violet-600",
          "bg-violet-700",
          "bg-violet-800",
          "bg-violet-900",
        ],
        purple: [
          "bg-purple-50",
          "bg-purple-100",
          "bg-purple-200",
          "bg-purple-300",
          "bg-purple-400",
          "bg-purple-500",
          "bg-purple-600",
          "bg-purple-700",
          "bg-purple-800",
          "bg-purple-900",
        ],
        fuchsia: [
          "bg-fuchsia-50",
          "bg-fuchsia-100",
          "bg-fuchsia-200",
          "bg-fuchsia-300",
          "bg-fuchsia-400",
          "bg-fuchsia-500",
          "bg-fuchsia-600",
          "bg-fuchsia-700",
          "bg-fuchsia-800",
          "bg-fuchsia-900",
        ],
        pink: [
          "bg-pink-50",
          "bg-pink-100",
          "bg-pink-200",
          "bg-pink-300",
          "bg-pink-400",
          "bg-pink-500",
          "bg-pink-600",
          "bg-pink-700",
          "bg-pink-800",
          "bg-pink-900",
        ],
        rose: [
          "bg-rose-50",
          "bg-rose-100",
          "bg-rose-200",
          "bg-rose-300",
          "bg-rose-400",
          "bg-rose-500",
          "bg-rose-600",
          "bg-rose-700",
          "bg-rose-800",
          "bg-rose-900",
        ],
      };
    },
  },
};
</script>