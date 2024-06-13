<script setup lang="ts">
import { ref, onMounted } from "vue";
import { themeChange } from "theme-change";
import { open, confirm, message } from "@tauri-apps/api/dialog";

// mounted
onMounted(() => {
  themeChange(false);
});

// ref
const showToast = ref(false);

const btnClick = () => {
  console.log("Clicked");
  showToast.value = true;
  setTimeout(() => (showToast.value = false), 3000);
};

const btnTestDialogConfirm = async () => {
  const confirmed = await confirm("This is test dialog", {
    title: "Test Dialog Confirm",
    type: "warning",
    okLabel: "Yes",
    cancelLabel: "No",
  });

  if (confirmed) {
    console.log("Confirmed");
    await message('You selected "Yes"', {
      title: "Test Dialog Message",
      type: "info",
    });
  } else {
    console.log("Cancelled");
    await message('You selected "No"', {
      title: "Test Dialog Message",
      type: "error",
    });
  }
};

const btnTestDialogOpen = async () => {
  const selected = await open({
    multiple: true,
    // multiple: false,
    filters: [
      {
        name: "Image",
        extensions: ["png", "jpeg"],
      },
    ],
  });
  if (Array.isArray(selected)) {
    // user selected multiple files
    console.log("Selected multiple files:", selected);
    await message("Selected multiple files:\n" + selected.join("\n") + "\n", {
      title: "Multiple Files",
      type: "info",
    });
  } else if (selected === null) {
    // user cancelled the selection
    await message("You cancelled the file selection", {
      title: "Cancelled",
      type: "info",
    });
  } else {
    // user selected a single file
    console.log("Selected single files:", selected);
    await message("Selected single files:\n" + selected + "\n", {
      title: "Multiple Files",
      type: "info",
    });
  }
};

// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
</script>
<template>
  <default-layout>
    <div
      class="container mx-auto flex h-[90%] max-w-screen-lg flex-col items-center justify-center border border-base-300 bg-base-100 p-5 shadow-xl"
    >
      <h1 class="mb-4 text-4xl font-bold">Welcome to Starter Template</h1>
      <div class="mb-8 text-sm tracking-wide">
        <ul class="list-inside list-disc">
          <li>Vite + Vue3 + Tailwind v3</li>
          <li>DaisyUI v4 + theme changer</li>
          <li>Iconify: mdi, ic, bxs, fluent, noto</li>
          <li>Auto import layout + components + icons</li>
          <li>Typescript</li>
        </ul>
      </div>
      <greet />
      <div class="grid grid-cols-2 place-content-center gap-4">
        <button-click @click="btnClick()">
          Click Toast
          <icons-mdi-cursor-default-click class="inline align-middle" />
        </button-click>
        <button-click @click="btnTestDialogConfirm()">
          Test Dialog
          <icons-mdi-message class="inline align-middle" />
        </button-click>
        <button-click @click="btnTestDialogOpen()">
          Open File Dialog
          <icons-mdi-folder class="inline align-middle" />
        </button-click>
        <button
          class="btn btn-neutral text-neutral-content"
          data-toggle-theme="dark,light"
        >
          Change Theme
          <icons-mdi-theme-light-dark class="inline align-middle" />
        </button>
      </div>
      <div v-if="showToast" class="toast toast-end">
        <div class="alert alert-success shadow-xl">
          <span>This is toast</span>
        </div>
      </div>
    </div>
  </default-layout>
</template>
