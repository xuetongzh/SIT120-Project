<template>
  <div class="item">
    <div class="item-row">
      <span class="material-icons material-icons-outlined"> event </span>
      {{ date }}
    </div>

    <div class="item-row">
      <span class="material-icons material-icons-outlined"> schedule </span>
      {{ startTime }} ~ {{ endTime }}
    </div>

    <div>{{ content }}</div>

    <div class="item-operate-box">
      <span
        class="material-icons material-icons-outlined"
        @click="$emit('delete')"
      >
        delete
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    date: String,
    startTime: String,
    endTime: String,
    content: String
  }
};
</script>