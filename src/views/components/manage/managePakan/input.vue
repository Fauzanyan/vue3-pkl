<template>
    <div class="layout-px-spacing dash_1 mx-2 my-3">
        <teleport to="#breadcrumb">
            <ul class="navbar-nav flex-row">
                <li>
                    <div class="page-header">
                        <nav class="breadcrumb-one" aria-label="breadcrumb">
                            <ol class="breadcrumb">
                                <li class="breadcrumb-item active" aria-current="page"><span>Manage Pakan</span></li>
                            </ol>
                        </nav>
                    </div>
                </li>
            </ul>
        </teleport>

        <div class="container">
            <div id="PemupukanDanPemberianMineral" class="col-lg-12">
                <div class="statbox panel box box-shadow">
                    <div class="panel-heading">
                        <div class="row">
                            <div class="col-xl-12 col-md-12 col-sm-12 col-12">
                                <h4>Tambah Data Pakan</h4>
                            </div>
                        </div>
                    </div>
                    <div class="panel-body">
                        <form class="form-vertical" action="#">
                            <div class="box-wrap">
                                <div class="form-group">
                                    <label class="control-label">Photo:</label>
                                    <div class="custom-file-container">
                                        <div class="invoice-logo">
                                            <div class="upload pe-md-5">
                                                <input ref="fl_profile" type="file" class="d-none" accept="image/*" @change="change_file" />
                                                <img
                                                    v-if="selected_file"
                                                    :src="selected_file ? selected_file : require('@/assets/images/user-profile.jpeg')"
                                                    alt="profile"
                                                    class="profile-preview"
                                                    @click="$refs.fl_profile.click()"
                                                />
                                                <div v-else class="profile-preview upload-preview text-center border" @click="$refs.fl_profile.click()">
                                                    <div class="my-2">
                                                        <svg
                                                            xmlns="http://www.w3.org/2000/svg"
                                                            width="50"
                                                            height="50"
                                                            viewBox="0 0 24 24"
                                                            fill="none"
                                                            stroke="currentColor"
                                                            stroke-width="2"
                                                            stroke-linecap="round"
                                                            stroke-linejoin="round"
                                                            class="feather feather-upload-cloud"
                                                        >
                                                            <polyline points="16 16 12 12 8 16"></polyline>
                                                            <line x1="12" y1="12" x2="12" y2="21"></line>
                                                            <path d="M20.39 18.39A5 5 0 0 0 18 9h-1.26A8 8 0 1 0 3 16.3"></path>
                                                            <polyline points="16 16 12 12 8 16"></polyline>
                                                        </svg>
                                                    </div>
                                                    <div class="mt-2">Click to Upload Picture/Logo</div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="box-wrap">
                                <div class="form-group">
                                    <label class="control-label">Nama Tambak:</label>
                                    <multiselect v-model="inputs['input1']" :options="options1" :searchable="true" placeholder="Choose..." selected-label="" select-label="" deselect-label="">
                                    </multiselect>
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Tanggal dan Jam Input:</label>
                                    <div class="mb-0">
                                        <flat-pickr v-model="date2" :config="{ enableTime: true, dateFormat: 'Y-m-d H:i' }" class="form-control flatpickr active"></flat-pickr>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Asal Pakan:</label>
                                    <multiselect
                                        v-model="inputs['input2']"
                                        :options="options2"
                                        :searchable="true"
                                        placeholder="Choose..."
                                        selected-label=""
                                        select-label=""
                                        deselect-label=""
                                    ></multiselect>
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Merk Pakan:</label>
                                    <input type="text" name="merek_pakana" class="form-control" placeholder="Masukan Merk Pakan" />
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Harga Pakan(Rp):</label>
                                    <input type="number" name="harga_pakana" class="form-control" v-maska="'###################'" placeholder="Masukan Harga Pakan (Rp)" />
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Kode Pakan:</label>
                                    <input type="text" name="kode_pakana" class="form-control" placeholder="Masukan Kode Pakan" />
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Pakan Batch Id:</label>
                                    <input type="text" name="" class="form-control" placeholder="Masukan Pakan Batch ID" />
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Jenis Butiran:</label>
                                    <multiselect
                                        v-model="inputs['input3']"
                                        :options="options3"
                                        :searchable="true"
                                        placeholder="Choose..."
                                        selected-label=""
                                        select-label=""
                                        deselect-label=""
                                    ></multiselect>
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Tanggal Beli:</label>
                                    <div class="mb-0">
                                        <flat-pickr v-model="date1" class="form-control flatpickr active"> </flat-pickr>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Ukuran (Kg) / karung:</label>
                                    <input type="number" class="form-control" v-maska="'##########################'" placeholder="Masukan Ukuran(Kg) / Karung" />
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Jumlah Karung:</label>
                                    <input type="number" name="" class="form-control" v-maska="'##########################'" placeholder="Masukan Jumlah Karung" />
                                </div>
                                <div class="form-group">
                                    <label class="control-label">Status:</label>
                                    <multiselect
                                        v-model="inputs['input4']"
                                        :options="options4"
                                        :searchable="true"
                                        placeholder="Choose..."
                                        selected-label=""
                                        select-label=""
                                        deselect-label=""
                                    ></multiselect>
                                </div>
                            </div>
                            <div class="submit">
                                <input type="submit" value="Simpan" class="btn btn-submit mt-3" />
                                <router-link to="/manage-pakan" @click="toggleMobileMenu" class="btn btn-kembali mt-3"> Kembali</router-link>
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

    const options1 = ref(['Tambak a', 'Tambak b']);
    const inputs = ref({
        input1: [],
        input2: [],
        input3: [],
        input4: [],
        input5: [],
    });
    const options2 = ref(['Indonesia']);
    const options3 = ref(['Mesh (tepung)', 'Crumble (granula)', 'Pelet']);
    const options4 = ref(['Aktif', 'Tidak aktif']);

    const code_arr = ref([]);
    const form1 = ref({ name: '' });
    const is_submit_form1 = ref(false);
    const form2 = ref({ email: '' });
    const is_submit_form2 = ref(false);
    const form3 = ref({ select: '' });
    const is_submit_form3 = ref(false);
    const form4 = ref({ first_name: 'Shaun', last_name: 'Park', username: '', city: '', state: '', zip: '', is_terms: false });
    const is_submit_form4 = ref(false);
    const form5 = ref({ first_name: 'Shaun', last_name: 'Park', username: '', city: '', state: '', zip: '', is_terms: false });
    const is_submit_form5 = ref(false);
    const form6 = ref({ first_name: 'Shaun', last_name: 'Park', username: '', city: '', state: '', zip: '', is_terms: false });
    const is_submit_form6 = ref(false);

    const items = ref([]);
    const selected_file = ref(null);
    const params = ref({
        title: '',
        invoice_no: '',
        from: { name: '', email: '', address: '', phone: '' },
        to: { name: '', email: '', address: '', phone: '' },

        invoice_date: '',
        due_date: '',
        bank_info: { no: '', name: '', swift_code: '', country: '' },
        notes: '',
    });
    const currency_list = ref([]);
    const selected_currency = ref({ key: 'USD - US Dollar', thumb: 'flags/en.png' });
    const tax_type_list = ref([]);
    const selected_tax_type = ref({ key: 'None', value: null });
    const discount_list = ref([]);
    const selected_discount = ref({ key: 'None', value: null, type: '' });

    onMounted(() => {
        //set default data
        items.value.push({ id: 1, title: '', description: '', rate: 0, quantity: 0, amount: 100, is_tax: false });

        let dt = new Date();
        params.value.invoice_date = JSON.parse(JSON.stringify(dt));
        dt.setDate(dt.getDate() + 5);
        params.value.due_date = dt;

        //currency list
        currency_list.value = [
            { key: 'USD - US Dollar', thumb: 'flags/en.png' },
            { key: 'GBP - British Pound', thumb: 'flags/gbp.png' },
            { key: 'IDR - Indonesian Rupiah', thumb: 'flags/idr.png' },
            { key: 'INR - Indian Rupee', thumb: 'flags/inr.png' },
            { key: 'BRL - Brazilian Real', thumb: 'flags/brl.png' },
            { key: 'EUR - Germany (Euro)', thumb: 'flags/de.png' },
            { key: 'TRY - Turkish Lira', thumb: 'flags/tr.png' },
        ];

        //tax type list
        tax_type_list.value = [
            { key: 'Deducted', value: 10 },
            { key: 'Per Item', value: 5 },
            { key: 'On Total', value: 25 },
            { key: 'None', value: null },
        ];

        //discount list
        discount_list.value = [
            { key: 'Percent', value: 10, type: 'percent' },
            { key: 'Flat Amount', value: 25, type: 'amount' },
            { key: 'None', value: null, type: '' },
        ];
    });

    const change_file = (event) => {
        selected_file.value = URL.createObjectURL(event.target.files[0]);
    };

    const add_item = () => {
        let max_id = 0;
        if (items.value && items.value.length) {
            max_id = items.value.reduce((max, character) => (character.id > max ? character.id : max), items.value[0].id);
        }
        items.value.push({ id: max_id + 1, title: '', description: '', rate: 0, quantity: 0, amount: 0, is_tax: false });
    };

    const remove_item = (item) => {
        items.value = items.value.filter((d) => d.id != item.id);
    };
</script>
