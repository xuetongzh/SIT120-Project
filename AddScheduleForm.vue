<template>
  <fieldset>
    <legend>Add a Schedule</legend>
    <div class="form-row">
      <label>Date:</label>
      <input type="date" v-model="date" />
    </div>

    <div class="form-row">
      <label>Start Time:</label>
      <input type="time" v-model="startTime" />
    </div>

    <div class="form-row">
      <label>End Time:</label>
      <input type="time" v-model="endTime" />
    </div>

    <div class="form-row">
      <label>Content:</label>
      <textarea v-model="content"></textarea>
    </div>

    <div class="btn-container">
      <button class="default-btn" @click="clickCancelBtn">Cancel</button>
      <button class="primary-btn" @click="clickConfirmBtn">Confirm</button>
    </div>
  </fieldset>
</template>

<script>
export default {
  data() {
    return {
      date: undefined,
      startTime: undefined,
      endTime: undefined,
      content: undefined
    };
  },

  methods: {
    clickCancelBtn() {
      this.$emit("onCancel");
    },
    clickConfirmBtn() {
      const { date, startTime, endTime, content } = this;
      if (!date || !startTime || !endTime || !content) {
        window.alert("Please fill in all fields.");
      }
      this.$emit("onConfirm", {
        date,
        startTime,
        endTime,
        content
      });
    }
  }
};
</script>