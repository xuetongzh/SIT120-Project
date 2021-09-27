<template>
  <div id="app">
    <app-header>
      <img
        slot="avatar"
        src="./assets/profile.jpeg"
        alt="Account icon"
        class="profile-img"
      />
    </app-header>

    <main>
      <div class="create-form">
        <div class="add-btn-box" v-if="!isAddingSchedule">
          <add-schedule-btn @add="clickAddScheduleBtn" />
        </div>

        <add-schedule-form
          v-if="isAddingSchedule"
          @onCancel="handleCancelAdd"
          @onConfirm="handleConfirmAdd"
        ></add-schedule-form>
      </div>

      <div class="search-form">
        <search-form
          :date="searchForm.date"
          :content="searchForm.content"
          @update:date="(v) => (this.searchForm.date = v)"
          @update:content="(v) => (this.searchForm.content = v)"
        />
      </div>

      <div class="list">
        <schedule-item
          v-for="(item, index) in searchedList"
          :key="item.content"
          v-bind="item"
          @delete="deleteItem(index)"
        >
        </schedule-item>
      </div>
    </main>
  </div>
</template>

<script>
import AppHeader from "./components/Header.vue";
import AddScheduleBtn from "./components/AddScheduleBtn";
import AddScheduleForm from "./components/AddScheduleForm";
import SearchForm from "./components/SearchForm";
import ScheduleItem from "./components/ScheduleItem.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AddScheduleBtn,
    AddScheduleForm,
    SearchForm,
    ScheduleItem
  },
  data() {
    return {
      isAddingSchedule: false,
      searchForm: {
        date: undefined,
        content: undefined
      },
      list: [
        {
          date: "2021-08-05",
          startTime: "09:00",
          endTime: "10:00",
          content: "Go to breakfast"
        },
        {
          date: "2021-08-06",
          startTime: "12:00",
          endTime: "13:00",
          content: "Go to lunch"
        }
      ]
    };
  },
  computed: {
    searchedList() {
      let list = this.list;
      if (this.searchForm.date) {
        list = list.filter(it => it.date === this.searchForm.date);
      }
      if (this.searchForm.content) {
        list = list.filter(it => it.content.includes(this.searchForm.content));
      }
      return list;
    }
  },
  methods: {
    clickAddScheduleBtn() {
      this.isAddingSchedule = true;
    },
    handleCancelAdd() {
      this.isAddingSchedule = false;
    },
    handleConfirmAdd(schedule) {
      this.isAddingSchedule = false;
      this.list.push(schedule);
    },
    deleteItem(index) {
      this.list.splice(index, 1);
    }
  }
};
</script>

<style>
</style>
