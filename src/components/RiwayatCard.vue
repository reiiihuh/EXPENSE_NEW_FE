<template>
  <div class="table-card">
    <div class="card-header">
      <span class="title">Laporan</span>
      <div class="controls">
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search"
          class="search-bar"
        />
        <div class="filter-dropdown">
          <button @click="toggleFilter" class="filter-btn">
            <span class="material-icons">tune</span><p>Filter</p>
          </button>
          <div v-if="showFilter" class="filter-menu">
            <div>
              <strong>Jenis</strong>
              <div>
                <input
                  type="checkbox"
                  id="operational"
                  value="Operational"
                  v-model="selectedTypes"
                />
                <label for="operational">Operational</label>
              </div>
              <div>
                <input
                  type="checkbox"
                  id="non-operational"
                  value="Non-Operational"
                  v-model="selectedTypes"
                />
                <label for="non-operational">Non-Operational</label>
              </div>
            </div>
            <div>
              <strong>Kategori</strong>
              <div>
                <input
                  type="checkbox"
                  id="honor"
                  value="Honor"
                  v-model="selectedCategories"
                />
                <label for="honor">Honor</label>
              </div>
              <div>
                <input
                  type="checkbox"
                  id="pribadi"
                  value="Pribadi"
                  v-model="selectedCategories"
                />
                <label for="pribadi">Pribadi</label>
              </div>
              <div>
                <input
                  type="checkbox"
                  id="listrik"
                  value="Listrik"
                  v-model="selectedCategories"
                />
                <label for="listrik">Listrik</label>
              </div>
              <div>
                <input
                  type="checkbox"
                  id="air"
                  value="Air"
                  v-model="selectedCategories"
                />
                <label for="air">Air</label>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="card-body">
      <div class="table-wrapper">
        <table>
          <thead>
            <tr>
              <th>Judul</th>
              <th>Tanggal</th>
              <th>Jenis</th>
              <th>Kategori</th>
              <th>Biaya</th>
              <th>Status</th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(item, index) in filteredTransactions"
              :key="index"
            >
              <td>{{ item.title }}</td>
              <td>{{ item.date }}</td>
              <td>{{ item.type }}</td>
              <td>{{ item.category }}</td>
              <td>{{ item.cost }}</td>
              <td :class="{'status-approved': item.status === 'Setuju', 'status-rejected': item.status === 'Ditolak'}">
                {{ item.status }}
              </td>
              <td>
                <span class="material-icons more-icon">more_horiz</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const transactions = ref([
  { title: 'Makan Siang', date: '00/00/00', type: 'Non-Operational', category: 'Pribadi', cost: 'Rp.0,00', status: 'Ditolak' },
  { title: 'Transportasi', date: '01/01/01', type: 'Operational', category: 'Listrik', cost: 'Rp.100,00', status: 'Setuju' },
  { title: 'Gaji Karyawan', date: '02/02/02', type: 'Operational', category: 'Honor', cost: 'Rp.200,00', status: 'Setuju' },
  { title: 'Tagihan Air', date: '03/03/03', type: 'Non-Operational', category: 'Air', cost: 'Rp.300,00', status: 'Setuju' },
]);

const searchQuery = ref('');
const selectedTypes = ref([]);
const selectedCategories = ref([]);
const showFilter = ref(false);

const toggleFilter = () => {
  showFilter.value = !showFilter.value;
};

const filteredTransactions = computed(() => {
  return transactions.value.filter((transaction) => {
    const matchesSearchQuery = transaction.title
      .toLowerCase()
      .includes(searchQuery.value.toLowerCase());
    const matchesType =
      selectedTypes.value.length === 0 ||
      selectedTypes.value.includes(transaction.type);
    const matchesCategory =
      selectedCategories.value.length === 0 ||
      selectedCategories.value.includes(transaction.category);
    return matchesSearchQuery && matchesType && matchesCategory;
  });
});
</script>

<style scoped lang="scss">
.table-card {
  width: 100%;
  max-width: 90rem;
  border: 2px solid var(--outline);
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);

  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;

    .title {
      font-size: 1.5rem;
      font-weight: bold;
    }

    .controls {
      display: flex;
      align-items: center;

      .search-bar {
        padding: 8px;
        border-radius: 8px;
        border: 2px solid var(--outline);
        margin-right: 16px;
        font-size: 1rem;
        outline: none;
      }

      .filter-dropdown {
        position: relative;

        .filter-btn {
          font-weight: 700;
          display: flex;
          align-items: center;
          padding: 0.4rem;
          border: 2px solid var(--outline);
          border-radius: 8px;
          background-color: var(--white);
          cursor: pointer;

          p {
            padding-left: 0.7rem;
          }
        }

        .filter-menu {
          position: absolute;
          right: 0;
          top: 2.8rem;
          background-color: var(--white);
          border: 2px solid var(--outline);
          border-radius: 8px;
          box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
          padding: 8px;
          width: 200px;
          z-index: 10;

          div {
            margin-bottom: 8px;
          }

          strong {
            display: block;
            margin-bottom: 4px;
          }

          label {
            margin-left: 4px;
          }
        }
      }
    }
  }

  .card-body {
    overflow-x: auto;

    .table-wrapper {
      max-height: 15.6rem;
      overflow-y: auto;
    }

    table {
      width: 100%;
      border-collapse: collapse;

      th {
        text-align: left;
        background-color: var(--inactive);
        padding: 0.5rem;
        font-weight: 500;
        padding-left: 0.7rem;
        color: var(--white);
        position: sticky;
        top: 0;
        z-index: 1;
      }

      td {
        padding: 0.8rem;
        border-top: 1px solid var(--outline);
        font-weight: 500;
      }

      .detail-btn {
        color: var(--inactive);
        cursor: pointer;
        font-weight: 600;
        padding-right: 1.4rem;
      }

      .more-icon {
        color: var(--inactive);
        cursor: pointer;
        transition: 0.2s ease-out;
        padding-left: 1.4rem;

        &:hover {
          color: var(--grey);
        }
      }
    }
  }
}

.status-approved {
  color: var(--primary); /* Green color */
}

.status-rejected {
  color: red; /* Red color */
}
</style>
