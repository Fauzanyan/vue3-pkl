<template>
    <div class="layout-px-spacing dash_1 mx-2 my-3">
        <teleport to="#breadcrumb">
            <ul class="navbar-nav flex-row">
                <li>
                    <div class="page-header">
                        <nav class="breadcrumb-one" aria-label="breadcrumb">
                            <ol class="breadcrumb">
                                <li class="breadcrumb-item active" aria-current="page"><span>Edit Data Saponin</span>
                                </li>
                            </ol>
                        </nav>
                    </div>
                </li>
            </ul>
        </teleport>

        <div class="container">
            <div id="saponin" class="col-lg-12">
                <div class="statbox panel box box-shadow">
                    <div class="panel-heading">
                        <div class="row">
                            <div class="col-xl-12 col-md-12 col-sm-12 col-12">
                                <h4>Edit Data Saponin</h4>
                            </div>
                        </div>
                    </div>
                    <div class="panel-body">
                        <form class="form-vertical" action="#">
                            <div class="box-wrap">
                                <div class="form-group">
                                    <label class="control-label">Nama Tambak:</label>
                                    <input type="text" name="nama_tambak" class="form-control"
                                        placeholder="Masukkan nama tambak" />
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Tanggal dan Jam Input:</label>
                                    <div class=" mb-0">
                                        <flat-pickr v-model="date2"
                                            :config="{ enableTime: true, dateFormat: 'Y-m-d H:i' }"
                                            class="form-control flatpickr active"></flat-pickr>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Kategori:</label>
                                    <multiselect v-model="inputs['input3']" :options="options1" :searchable="true"
                                        placeholder="Choose..." selected-label="" select-label="" deselect-label="">
                                    </multiselect>
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Jenis:</label>
                                    <input type="text" name="jenis" class="form-control"
                                        placeholder="Contoh data, Vit C, Vit A, pupuk amonia" />
                                </div>
                                <div class="form-group w-100">
                                    <label class="control-label">Keterangan:</label>
                                    <input type="text" name="keterangan" class="form-control"
                                        placeholder="Beri keterangan" />
                                </div>

                                <div class="form-group">
                                    <label class="control-label">Status</label>
                                    <multiselect v-model="inputs2['input3']" :options="options2" :searchable="true"
                                        placeholder="Choose..." selected-label="" select-label="" deselect-label="">
                                    </multiselect>
                                </div>
                            </div>
                            <div class="submit">
                                <input type="submit" value="Simpan" class="btn btn-submit mt-3" />
                                <router-link to="/saponin" @click="toggleMobileMenu" class="btn btn-kembali mt-3">
                                    Kembali</router-link>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import '@/assets/sass/scrollspyNav.scss';
import '@/assets/sass/forms/file-upload-with-preview.min.css';
import '@suadelabs/vue3-multiselect/dist/vue3-multiselect.css';
import '@/assets/sass/forms/file-upload-with-preview.min.css';
import highlight from '@/components/plugins/highlight.vue';

import flatPickr from 'vue-flatpickr-component';
import 'flatpickr/dist/flatpickr.css';

import Multiselect from '@suadelabs/vue3-multiselect';

import FileUploadWithPreview from 'file-upload-with-preview';

import { useMeta } from '@/composables/use-meta';
useMeta({ title: 'File Upload' });

const code_arr = ref([]);
const selected_file = ref(null);

const toggleCode = (name) => {
    if (code_arr.value.includes(name)) {
        code_arr.value = code_arr.value.filter((d) => d != name);
    } else {
        code_arr.value.push(name);
    }
};

const options1 = ref(['Saponin', 'Pupuk', 'Probiotik', 'Vitamin']);
const inputs = ref({
    input1: [],
    input2: [],
    input3: [],
    input4: [],
    input5: [],
});

const options2 = ref(['Aktif', 'Tidak Aktif']);
const inputs2 = ref({
    input1: [],
    input2: [],
    input3: [],
    input4: [],
    input5: [],
});

const change_file = (event) => {
    selected_file.value = URL.createObjectURL(event.target.files[0]);
};
</script>
