<template>
    <div class="layout-px-spacing">
        <teleport to="#breadcrumb">
            <ul class="navbar-nav flex-row">
                <li>
                    <div class="page-header">
                        <nav class="breadcrumb-one" aria-label="breadcrumb">
                            <ol class="breadcrumb">
                                <li class="breadcrumb-item active" aria-current="page"><span>Siklus Budidaya Air - Parameter Fisika</span></li>
                            </ol>
                        </nav>
                    </div>
                </li>
            </ul>
        </teleport>

        <div class="row layout-top-spacing">
            <div class="col-xl-12 col-lg-12 col-sm-12 layout-spacing">
                <div class="panel br-6 p-0">
                    <div class="custom-table">
                        <div class="panel-heading">
                            <div class="row">
                                <div class="col-xl-12 col-md-12 col-sm-12 col-12">
                                    <h4>Parameter Fisika</h4>
                                </div>
                            </div>
                        </div>
                        <div class="d-flex flex-row-reverse position-relative">
                            <router-link to="/budidaya-fisika/create" @click="toggleMobileMenu" class="btn mb-2 mx-3 tambah-data">Tambah Data</router-link>
                        </div>
                        <v-client-table :data="items" :columns="columns" :options="table_option">
                            <template #no="props" v-for="(item, index) in items">
                                {{ props.index }}
                            </template>

                            <template #actions="props">
                                <div class="table-controls d-flex no-wrap justify-content-center">
                                    <div class="px-2">
                                        <div @click="view_row(props.row)" style="cursor: pointer" title="View">
                                            <svg
                                                xmlns="http://www.w3.org/2000/svg"
                                                width="24"
                                                height="24"
                                                viewBox="0 0 24 24"
                                                fill="none"
                                                stroke="currentColor"
                                                stroke-width="2"
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                class="feather feather-eye"
                                            >
                                                <path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"></path>
                                                <circle cx="12" cy="12" r="3"></circle>
                                            </svg>
                                        </div>
                                    </div>
                                    <div class="px-2">
                                        <a href="/budidaya-fisika/edit" data-bs-toggle="tooltip" title="Edit">
                                            <svg
                                                xmlns="http://www.w3.org/2000/svg"
                                                width="24"
                                                height="24"
                                                viewBox="0 0 24 24"
                                                fill="none"
                                                stroke="currentColor"
                                                stroke-width="2"
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                class="feather feather-edit-2"
                                            >
                                                <path d="M17 3a2.828 2.828 0 1 1 4 4L7.5 20.5 2 22l1.5-5.5L17 3z"></path>
                                            </svg>
                                        </a>
                                    </div>
                                    <div class="px-2">
                                        <a href="javascript:void(0);" data-bs-toggle="tooltip" title="Delete">
                                            <svg
                                                xmlns="http://www.w3.org/2000/svg"
                                                width="24"
                                                height="24"
                                                viewBox="0 0 24 24"
                                                fill="none"
                                                stroke="currentColor"
                                                stroke-width="2"
                                                stroke-linecap="round"
                                                stroke-linejoin="round"
                                                class="feather feather-trash-2"
                                            >
                                                <polyline points="3 6 5 6 21 6"></polyline>
                                                <path d="M19 6v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2"></path>
                                                <line x1="10" y1="11" x2="10" y2="17"></line>
                                                <line x1="14" y1="11" x2="14" y2="17"></line>
                                            </svg>
                                        </a>
                                    </div>
                                </div>
                            </template>
                            <template #salary="props"> ${{ props.row.salary }} </template>
                        </v-client-table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { onMounted, ref } from 'vue';

    import { useMeta } from '@/composables/use-meta';
    useMeta({ title: 'Default Order Sorting Table' });

    const columns = ref(['no', 'Nama_Tambak', 'Nama_Kolam', 'Tanggal', 'Tinggi_Air_(cm)', 'Kecerahan_(cm)', 'Warna_Suhu_air_(celcius)', 'DOC', 'actions']);

    const items = ref([]);
    const table_option = ref({
        perPage: 10,
        perPageValues: [5, 10, 20, 50],
        skin: 'table table-hover',
        columnsClasses: { actions: 'actions text-center'},
        pagination: { nav: 'scroll', chunk: 5 },
        texts: {
            count: 'Showing {from} to {to} of {count}',
            filter: '',
            filterPlaceholder: 'Search...',
            limit: 'Results:',
        },
        sortable: ['no', 'Nama_Tambak', 'Nama_Kolam', 'Tanggal', 'Tinggi_Air_(cm)', 'Kecerahan_(cm)', 'Warna_Suhu_air_(celcius)', 'DOC'],
        sortIcon: {
            base: 'sort-icon-none',
            up: 'sort-icon-asc',
            down: 'sort-icon-desc',
        },
        resizableColumns: false,
    });

    onMounted(() => {
        bind_data();
    });

    const bind_data = () => {
        items.value = [
            {
                id: 1,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/01/25',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '25',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 2,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/02/15',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '25',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 3,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/03/05',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '35',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 4,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/04/23',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '35',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 5,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/05/19',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '35',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 6,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/06/01',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '35',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 7,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/06/29',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '25',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 8,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/07/25',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '25',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 9,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/08/20',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '25',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
            {
                id: 10,
                Nama_Tambak: 'Tambak',
                Nama_Kolam: 'Kolam B',
                Tanggal: '2022/09/10',
                'Tinggi_Air_(cm)': '25',
                'Kecerahan_(cm)': '25',
                'Warna_Suhu_air_(celcius)': 'null',
                DOC: 'null',
            },
        ];
    };

    const view_row = (item) => {
        new window.Swal({
            title: '<i>Parameter Fisika</i>',
            text: 'HALLO',
            html:
                '<p><b>Nama Tambak</b> : ' +
                item.Nama_Tambak +
                '</p>' +
                '<p><b>Nama Kolam</b> : ' +
                item.Nama_Kolam +
                '</p>' +
                '<p><b>Tanggal</b> : ' +
                item.Tanggal +
                '</p>' +
                '<p><b>DOC</b> : ' +
                item.DOC +
                '</p>',
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'+
            // '<p><b>Nama</b> : ' + item.nama + '</p>'
            // BUKA KOMENTAR JIKA BUTUH LEBIH BANYAK DATA
            // DIAKHIR TIDAK MENGGUNAKAN tanda +
            showCloseButton: true,
            focusConfirm: false,
            confirmButtonColor: '#4361ee',
            confirmButtonText: '<i class="flaticon-checked-1"></i> Oke',
            confirmButtonAriaLabel: 'Oke',

            padding: '2em',
        });
        // alert(' Name: ' + item.nama + ', MIN: ' + item.min + ', MAX: ' + item.max);
    };
</script>
