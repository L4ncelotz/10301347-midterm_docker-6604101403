<template>
  <q-page padding>
    <div class="text-h4 q-mb-md">
      Advanced Full-Stack Demo (Quasar + Express)
    </div>

    <!-- Git Workflow -->
    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Git Workflow</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(step, index) in gitSteps" :key="index">
            <q-item-section avatar>
              <q-badge>{{ index + 1 }}</q-badge>
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ step.title }}</q-item-label>
              <q-item-label caption>{{ step.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- Docker Concepts -->
    <q-card class="q-mb-md">
      <q-card-section>
        <div class="text-h6">Docker Concepts</div>
        <q-list bordered separator class="q-mt-sm">
          <q-item v-for="(item, index) in dockerItems" :key="index">
            <q-item-section>
              <q-item-label>{{ item.title }}</q-item-label>
              <q-item-label caption>{{ item.detail }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>

    <!-- New: API Data from Backend -->
    <q-card>
      <q-card-section>
        <div class="text-h6">Data from Backend API</div>
        <div v-if="loading" class="row justify-center q-pa-md">
             <q-spinner color="primary" size="2em" />
        </div>
        <q-list v-else bordered separator class="q-mt-sm">
          <q-item>
            <q-item-section>
              <q-item-label>Advanced Git</q-item-label>
              <q-item-label caption>{{ apiData.git?.detail || 'No data' }}</q-item-label>
            </q-item-section>
          </q-item>
          <q-item>
            <q-item-section>
              <q-item-label>Advanced Docker</q-item-label>
              <q-item-label caption>{{ apiData.docker?.detail || 'No data' }}</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
        <q-btn v-if="!loading" color="primary" @click="fetchData" class="q-mt-md">Refresh Data</q-btn>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const gitSteps = [
  { title: 'Feature Branch', detail: 'Develop features in isolated branches' },
  { title: 'Pull Request', detail: 'Code review and discussion before merging' },
  { title: 'Merge', detail: 'Integrate changes into main branch' }
];

const dockerItems = [
  { title: 'Images', detail: 'Blueprints for containers' },
  { title: 'Containers', detail: 'Running instances of images' },
  { title: 'Volumes', detail: 'Persist data outside containers' }
];

const apiData = ref({ git: {}, docker: {} });
const loading = ref(true);

const fetchData = async () => {
  loading.value = true;
  try {
    const apiUrl = import.meta.env.VITE_API_URL || 'http://localhost:3000';
    console.log('Fetching from:', apiUrl); // Debugging
    const response = await axios.get(`${apiUrl}/api/demo`);
    apiData.value = response.data;
  } catch (error) {
    console.error('API Error:', error);
    apiData.value = {
        git: { detail: `Error: ${error.message}` },
        docker: { detail: 'Please check if backend is running' }
    };
  } finally {
    loading.value = false;
  }
};

onMounted(fetchData);
</script>
