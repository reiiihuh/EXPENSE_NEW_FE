<template>
  <div class="kelola-laporan">
    <!-- <h1>Kelola Laporan</h1> -->
    <div class="laporan-container">
      <table class="laporan-table">
        <thead>
          <tr>
            <th>No.</th>
            <th>Gambar</th>
            <th>Judul</th>
            <th>Tanggal</th>
            <th>Jenis</th>
            <th>Pelapor</th>
            <th>Status</th>
            <th>Aksi</th>
            <th>Keterangan</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in laporanData" :key="index">
            <td>{{ index + 1 }}</td>
            <td>
              <img :src="item.gambar" alt="gambar laporan" class="gambar-laporan" />
            </td>
            <td>{{ item.judul }}</td>
            <td>{{ item.tanggal }}</td>
            <td>{{ item.jenis }}</td>
            <td>{{ item.pelapor }}</td>
            <td>
              <span :class="statusClass(item.selectedAction)">
                {{ item.status }}
              </span>
            </td>
            <td>
              <select v-if="item.status === 'Pending'" v-model="item.selectedAction">
                <option value="" disabled>Status</option>
                <option value="Setuju">Setuju</option>
                <option value="Tolak">Tolak</option>
              </select>
            </td>
            <td>
              <input
                v-if="item.status === 'Pending'"
                v-model="item.komentar"
                type="text"
                placeholder="Beri komentar.."
              />
              <p v-else>{{ item.komentar }}</p>
            </td>
            <td>
              <button
                v-if="item.status === 'Pending'"
                class="save-btn"
                @click="saveLaporan(index)"
              >
                Save
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      laporanData: [
        {
          gambar: 'https://via.placeholder.com/50',
          judul: 'Belanja',
          tanggal: '01/01/2024',
          jenis: 'Operasional',
          pelapor: 'Bendahara',
          status: 'Pending',
          komentar: '',
          selectedAction: '',
        },
        {
          gambar: 'https://via.placeholder.com/50',
          judul: 'Belanja',
          tanggal: '02/01/2024',
          jenis: 'Operasional',
          pelapor: 'Bendahara',
          status: 'Setuju',
          komentar: 'Disetujui',
          selectedAction: 'Setuju',
        },
      ],
    };
  },
  methods: {
    saveLaporan(index) {
      const laporan = this.laporanData[index];
      if (laporan.selectedAction && laporan.komentar) {
        laporan.status = 'Setuju';
      } else {
        alert('Silakan pilih status dan beri komentar.');
      }
    },
    statusClass(action) {
      if (action === 'Setuju') return 'approved';
      if (action === 'Tolak') return 'rejected';
      return '';
    },
  },
};
</script>

<style scoped>
.kelola-laporan {
  padding: 1rem;
}

h1 {
  color: var(--green-kkc);
  font-weight: bold;
}

.laporan-container {
  border: 2px solid var(--border-gray);
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.laporan-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 1rem;
}

.laporan-table th,
.laporan-table td {
  padding: 10px;
  border: 1px solid #ccc;
  text-align: center;
  background-color: #fff;
}

.laporan-table th {
  background-color: var(--header-background);
  font-weight: bold;
  color: #333;
}

.gambar-laporan {
  width: 50px;
  height: 50px;
  border-radius: 8px;
  background-color: #f0f0f0;
}

select,
input {
  padding: 5px;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 100%;
}

.save-btn {
  padding: 5px 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.save-btn:hover {
  background-color: #0056b3;
}

.pending {
  color: orange;
}

.approved {
  color: green;
}

.rejected {
  color: red;
}

.status-btn {
  padding: 5px 10px;
  border-radius: 5px;
  color: white;
}

.status-btn.approved {
  background-color: green;
}

.status-btn.rejected {
  background-color: red;
}
</style>
