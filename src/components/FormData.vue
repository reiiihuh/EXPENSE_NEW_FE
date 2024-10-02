<template>
    <div class="pencatatan-pengeluaran">
      <!-- <h1>Pencatatan Pengeluaran</h1> -->
      
      <div class="form-container">
        <!-- Box untuk input foto -->
        <div class="photo-box">
          <div class="photo-placeholder">
            <span class="material-icons">add_photo_alternate</span>
            <p>Tambah Foto</p>
          </div>
          <span class="material-icons delete-icon" @click="deletePhoto">delete</span>
        </div>
        
        <!-- Form input -->
        <div class="form-inputs">
          <input type="text" placeholder="Judul" v-model="formData.title" />
          <input type="date" placeholder="Tanggal" v-model="formData.date" />
          <select v-model="formData.type">
            <option value="" disabled selected>Jenis</option>
            <option value="operasional">Operasional</option>
            <option value="non-operasional">Non-Operasional</option>
          </select>
          <select v-model="formData.category">
            <option value="" disabled selected>Kategori</option>
            <option value="pribadi">Pribadi</option>
            <option value="listrik">Listrik</option>
            <option value="air">Air</option>
          </select>
          <!-- <input type="text" placeholder="Nama Pelapor" v-model="formData.reporterName" /> -->
          <!-- <select v-model="formData.role">
            <option value="" disabled selected>Role</option>
            <option value="admin">Admin</option>
            <option value="user">User</option>
          </select> -->
          <input type="text" placeholder="Biaya" v-model="formData.cost" />
        </div>
      </div>
      <div class="description-container">
      <textarea
        v-model="description"
        @input="updateCharCount"
        placeholder="Deskripsi"
        maxlength="500"
      ></textarea>
    <div class="char-count">{{ charCount }} karakter tersisa</div>
      </div>
      <div class="form-actions">
        <button class="btn-cancel" @click="cancel">Cancel</button>
        <button class="btn-save" @click="save">Simpan</button>
      </div>
    </div>
    
  </template>
  
<script setup>
  import { reactive } from 'vue';
  
  const formData = reactive({
    title: '',
    date: '',
    type: '',
    category: '',
    reporterName: '',
    role: '',
    cost: ''
  });
  
  function deletePhoto() {
    console.log('Foto dihapus');
  }
  
  function cancel() {
    console.log('Input dibatalkan');
  }
  
  function save() {
    console.log('Data disimpan', formData);
  }
  
  // hitung sisa karakter
  import { ref } from 'vue';

  const description = ref('');
  const maxChars = 500;
  const charCount = ref(maxChars);

  const updateCharCount = () => {
    charCount.value = maxChars - description.value.length;
  };

</script>
  
  <style scoped lang="scss">
  .pencatatan-pengeluaran {
    padding: 1.4rem;
  
    h1 {
      color: var(--green-kkc);
      font-weight: 700;
    }
  
    .form-container {
      display: flex;
      gap: 1rem;
      margin-top: 1rem;
  
      .photo-box {
        width: 24rem;
        height: 15rem;
        border: 2px solid var(--outline);
        border-radius: 8px;
        position: relative;
        padding: 1rem;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
  
        .photo-placeholder {
          text-align: center;
          color: var(--inactive);
          
          .material-icons {
            font-size: 2rem;
            padding-top: 4.8rem;
          }
        }
  
        .delete-icon {
          position: absolute;
          top: 8px;
          right: 8px;
          color: var(--inactive);
          cursor: pointer;
          transition: 0.2s ease-out;
  
          &:hover {
            color: red;
          }
        }
      }
  
      .form-inputs {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 1rem;
        width: 100%;
        height: 1rem;
  
        input, select {
          width: 100%;
          padding: 0.8rem;
          border: 2px solid var(--outline);
          border-radius: 8px;
          font-weight: 600;
        }
      }
    }
  
    .form-actions {
      margin-top: 1.5rem;
      display: flex;
      gap: 1rem;
      
      .btn-cancel {
        background-color: red;
        color: white;
        padding: 0.8rem 1.5rem;
        border: none;
        border-radius: 4px;
        cursor: pointer;
      }
  
      .btn-save {
        background-color: var(--green-kkc);
        color: white;
        padding: 0.8rem 1.5rem;
        border: none;
        border-radius: 4px;
        cursor: pointer;
      }
    }
    .description-container {
    position: relative;
    
    textarea {
      width: 19rem;
      padding: 0.8rem;
      margin-top: 1rem;
      border: 2px solid var(--outline);
      border-radius: 8px;
      resize: none;
      height: 100px;
    }

    .char-count {
      text-align: left;
      font-size: 0.875rem;
      color: #6b7280;
      margin-top: 5px;
    }
    }
}
  </style>
  