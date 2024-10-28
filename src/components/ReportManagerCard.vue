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
            <th>Biaya</th>
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
            <td>{{ item.biaya }}</td>
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
          biaya: 'Rp.50.000',
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
          biaya: 'Rp.20.000',
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
  padding: 0.2rem;
  border-radius: 10px;
}

h1 {
  color: var(--green-kkc);
  font-weight: bold;
  font-size: 24px;
  margin-bottom: 20px;
  text-align: center;
}

.laporan-container {
  border: 2px solid var(--outline);
  border-radius: 8px;
  padding: 1rem;
  background-color: #fff;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.03);
}

.laporan-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 1.5rem;
}

/* .laporan-table th, */
.laporan-table td {
  padding: 10px 10px;
  border-bottom: 2px solid #eee;
  text-align: left;
  font-size: 0.9em;
  /* background-color: #fff; */
}

.laporan-table th {
  padding: 10px 10px;
  background-color: var(--outline);
  color: #444;
  font-weight: 700;
  text-transform: uppercase;
  text-align: left;
  font-size: 0.9em;
  /* letter-spacing: 1px; */
}

.laporan-table td {
  vertical-align: middle;
}

.laporan-table tbody tr:hover {
  background-color: #f2f2f2;
  transition: background-color 0.3s ease;
}

.laporan-table th:first-child,
.laporan-table td:first-child {
  border-radius: 8px 0 0 8px;
}

.laporan-table th:last-child,
.laporan-table td:last-child {
  border-radius: 0 8px 8px 0;
}

.gambar-laporan {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 6px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.gambar-laporan:hover {
  transform: scale(1.05);
}

select,
input {
  padding: 8px;
  border-radius: 5px;
  border: 1px solid #ccc;
  width: 100%;
  margin-bottom: 1rem;
  font-size: 14px;
}

.save-btn {
  margin-top: -0.4rem;
  padding: 8px 15px;
  background-color: var(--blue-coe);
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s ease;
}

.save-btn:hover {
  background-color: #0056b3;
}

.pending {
  color: #ff9800;
}

.approved {
  color: #4caf50;
}

.rejected {
  color: #f44336;
}

.status-btn {
  padding: 8px 15px;
  border-radius: 5px;
  font-size: 13px;
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.status-btn.approved {
  background-color: #4caf50;
}

.status-btn.rejected {
  background-color: #f44336;
}

.status-btn.approved:hover {
  background-color: #388e3c;
}

.status-btn.rejected:hover {
  background-color: #d32f2f;
}
</style>

