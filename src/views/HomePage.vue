<template>
  <ion-page>
    <ion-header>
      <ion-toolbar color="tertiary">
        <ion-title>Tugas Cuaca Jakarta</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content class="ion-padding">
      <div class="container">
        <h2>🌤️ Cuaca Jakarta</h2>
        <p class="description">Prakiraan suhu per jam dari Open-Meteo API</p>

        <div class="info">
          <p><strong>Lokasi:</strong> Jakarta</p>
          <p>{{ status }}</p>
        </div>

        <div class="table-wrapper">
          <table>
            <thead>
              <tr>
                <th>No.</th>
                <th>Waktu Pengukuran</th>
                <th>Suhu (°C)</th>
              </tr>
            </thead>

            <tbody>
              <tr v-if="loading">
                <td colspan="3">Memuat data...</td>
              </tr>

              <tr v-else-if="error">
                <td colspan="3">{{ error }}</td>
              </tr>

              <tr v-else v-for="(item, index) in weatherData" :key="item.time">
                <td>{{ index + 1 }}</td>
                <td>{{ item.time.replace("T", " ") }}</td>
                <td>
                  {{
                    item.temperature === null
                      ? "Tidak tersedia"
                      : item.temperature + " °C"
                  }}
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <footer>
          Sumber data:
          <a
            href="https://open-meteo.com/"
            target="_blank"
            rel="noopener noreferrer"
          >
            Open-Meteo API
          </a>
        </footer>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup>
import { ref, onMounted } from "vue";
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
} from "@ionic/vue";

const apiUrl =
  "https://api.open-meteo.com/v1/forecast?latitude=-6.2&longitude=106.8&hourly=temperature_2m&timezone=Asia%2FBangkok";

const weatherData = ref([]);
const loading = ref(true);
const error = ref("");
const status = ref("Sedang mengambil data cuaca...");

async function getWeather() {
  try {
    const response = await fetch(apiUrl);

    if (!response.ok) {
      throw new Error("Gagal mengambil data dari API.");
    }

    const data = await response.json();
    const times = data.hourly.time;
    const temperatures = data.hourly.temperature_2m;

    weatherData.value = times.map((time, index) => ({
      time,
      temperature: temperatures[index],
    }));

    status.value = `Berhasil menampilkan ${weatherData.value.length} data temperatur.`;
  } catch (err) {
    error.value = "Data gagal dimuat. Periksa koneksi internet.";
    status.value = "Terjadi kesalahan saat mengambil data.";
    console.error(err);
  } finally {
    loading.value = false;
  }
}

onMounted(() => {
  getWeather();
});
</script>

<style scoped>
.container {
  padding: 10px;
  color: #4a148c;
}

h2 {
  text-align: center;
  color: #880e4f;
}

.description {
  text-align: center;
  color: #880e4f;
}

.info {
  background: #f8bbd0;
  padding: 12px;
  border-radius: 8px;
  margin: 20px 0;
}

.info p {
  margin: 5px 0;
}

.table-wrapper {
  max-height: 400px;
  overflow: auto;
  border: 1px solid #f8bbd0;
  border-radius: 8px;
}

table {
  width: 100%;
  border-collapse: collapse;
  background: white;
}

th,
td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #f8bbd0;
}

th {
  position: sticky;
  top: 0;
  background: #f48fb1;
  color: white;
  z-index: 1;
}

tbody tr:nth-child(even) {
  background: #fff8fa;
}

footer {
  margin-top: 20px;
  text-align: center;
  color: #880e4f;
}

a {
  color: #880e4f;
}

@media (max-width: 480px) {
  th,
  td {
    padding: 8px 6px;
    font-size: 12px;
  }
}
</style>
