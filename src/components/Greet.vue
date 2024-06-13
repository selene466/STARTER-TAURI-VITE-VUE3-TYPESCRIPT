<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";
import { writeText, readText } from "@tauri-apps/api/clipboard";

const greetMsg = ref("");
const name = ref("");
const textBox = ref("");

const greet = async () => {
  // Learn more about Tauri commands at https://tauri.app/v1/guides/features/command
  if (name.value) greetMsg.value = await invoke("greet", { name: name.value });
  else greetMsg.value = "";
};

const btnPasteText = async () => {
  const clipboardReadText = await readText();
  if (clipboardReadText !== null) {
    textBox.value = clipboardReadText;
    console.log("Pasted Text: " + clipboardReadText);
  }
};

const btnCopyText = async () => {
  await writeText(name.value);
  console.log("Copied to clipboard");
};
</script>

<template>
  <form class="row" @submit.prevent="greet">
    <div class="mb-2 flex w-full items-center gap-2.5">
      <input
        v-model="name"
        type="text"
        placeholder="Enter a name..."
        class="input input-bordered w-full"
      />
      <button
        type="submit"
        class="btn btn-primary font-bold text-primary-content"
      >
        Greet
      </button>
    </div>
    <div class="mb-4 flex w-full flex-wrap items-center justify-center gap-2.5">
      <div
        class="w-full rounded-xl border-2 border-dashed border-accent bg-neutral p-2 text-neutral-content"
      >
        <span v-if="textBox">
          {{ textBox }}
        </span>
        <span v-else>clipboard test</span>
      </div>
      <button
        @click="btnCopyText()"
        type="button"
        class="btn btn-primary btn-xs font-bold text-primary-content"
      >
        <icons-mdi-clipboard-file class="inline align-middle" />
        Copy Name
      </button>
      <button
        @click="btnPasteText()"
        type="button"
        class="btn btn-primary btn-xs font-bold text-primary-content"
      >
        <icons-mdi-clipboard-arrow-down class="inline align-middle" />
        Paste Clipboard
      </button>
      <button
        @click="textBox = 'test clipboard'"
        type="button"
        class="btn btn-primary btn-xs font-bold text-primary-content"
      >
        <icons-mdi-restore class="inline align-middle" />
        Clear
      </button>
    </div>
  </form>

  <p v-if="greetMsg" class="mb-4 tracking-wide">{{ greetMsg }}</p>
</template>
