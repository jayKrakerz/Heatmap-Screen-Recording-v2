<template>
  <div class="border-t border-gray50">
    <div class="flex">
      <SideBar />
      <div class="w-full">
        <!-- Pass recordingsCount and selectedRecording as props to AppNav -->
        <AppNav :recordingsCount="recordingsCount" :selectedRecording="selectedRecording"
          @update:selectedRecording="selectedRecording = $event" @unselectRecording="selectedRecording = null"
          @selectPreviousRecording="selectPreviousRecording" @selectNextRecording="selectNextRecording" />

        <!-- Listen for updateRecordingsCount and selectRecording events from RecordingsTable -->
        <RecordingsTable :selectedRecording="selectedRecording" @updateRecordingsCount="updateRecordingsCount"
          @selectRecording="setSelectedRecording" />
      </div>
    </div>
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue';
import RecordingsTable from "./components/RecordingsTable.vue";
import SideBar from "./components/SideBar.vue";
import AppNav from "./components/AppNav.vue";
import records, { Record } from './lib/recordingsData';
import { useRecordings } from './composable/useRecordings';

const {
  filteredSortedRecords,
  selectedRecording,
  selectPreviousRecording,
  selectNextRecording,
} = useRecordings(records);

const recordingsCount = ref(filteredSortedRecords.value.length);

function updateRecordingsCount(count: number) {
  recordingsCount.value = count;
}

function setSelectedRecording(record: Record) {
  selectedRecording.value = record;
}
</script>
