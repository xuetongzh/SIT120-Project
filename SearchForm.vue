<template>
  <div class="search-form">
    <fieldset>
      <legend>Search</legend>
      <div class="form-row">
        <label>Date:</label>
        <input
          type="date"
          :value="date"
          @change="$emit('update:date', $event.target.value)"
        />
      </div>

      <div class="form-row">
        <label>Content:</label>
        <input
          :value="content"
          @input="$emit('update:content', $event.target.value)"
        />
      </div>
    </fieldset>
  </div>
</template>

<script>
export default {
  props: {
    date: String,
    content: String
  }
};
</script>