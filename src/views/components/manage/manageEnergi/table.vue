<template>
    <div class="layout-px-spacing">
        <teleport to="#breadcrumb">
            <ul class="navbar-nav flex-row">
                <li>
                    <div class="page-header">
                        <nav class="breadcrumb-one" aria-label="breadcrumb">
                            <ol class="breadcrumb">
                                <li class="breadcrumb-item active" aria-current="page"><span>Manage Energi</span></li>
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
                                    <h4>Manage Energi</h4>
                                </div>
                            </div>
                        </div>
                        <div class="d-flex flex-row-reverse position-relative">
                            <router-link to="/manage-energi/create" @click="toggleMobileMenu" class="btn mb-2 mx-3 tambah-data">Tambah Data</router-link>
                        </div>

                        <v-client-table :data="items" :columns="columns" :options="table_option">
                            <template #no="props" v-for="index in items">
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
                                        <router-link to="/manage-energi/edit" data-bs-toggle="tooltip" title="Edit">
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
                                        </router-link>
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

    const columns = ref(['no', 'nama_tambak', 'tanggal', 'bulan', 'sumber_energi', 'actions']);
    const items = ref([]);
    const table_option = ref({
        perPage: 10,
        perPageValues: [5, 10, 20, 50],
        skin: 'table table-hover',
        columnsClasses: { no: 'no text-end', actions: 'actions text-center', tanggal: 'text-center', sumber_energi: 'text-end', konsumsi_listrik: 'text-end' },
        pagination: { nav: 'scroll', chunk: 5 },
        texts: {
            count: 'Showing {from} to {to} of {count}',
            filter: '',
            filterPlaceholder: 'Search...',
            limit: 'Results:',
        },
        sortable: ['nama_tambak', 'tanggal', 'bulan', 'sumber_energi'],
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
                nama_tambak: 'Tambak a',
                tanggal: '2022/01/25',
                bulan: 'Januari',
                sumber_energi: 2000,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 2,
                nama_tambak: 'Tambak b',
                tanggal: '2022/01/28',
                bulan: 'Januari',
                sumber_energi: 2453,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 3,
                nama_tambak: 'Tambak c',
                tanggal: '2022/02/01',
                bulan: 'Februari',
                sumber_energi: 2066,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 4,
                nama_tambak: 'Tambak d',
                tanggal: '2022/02/05',
                bulan: 'Februari',
                sumber_energi: 2002,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 5,
                nama_tambak: 'Tambak e',
                tanggal: '2022/02/08',
                bulan: 'Februari',
                sumber_energi: 2233,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 6,
                nama_tambak: 'Tambak f',
                tanggal: '2022/02/12',
                bulan: 'Februari',
                sumber_energi: 2049,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 7,
                nama_tambak: 'Tambak g',
                tanggal: '2022/02/19',
                bulan: 'Februari',
                sumber_energi: 2034,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 8,
                nama_tambak: 'Tambak  h',
                tanggal: '2022/02/23',
                bulan: 'Februari',
                sumber_energi: 2768,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 9,
                nama_tambak: 'Tambak i',
                tanggal: '2022/02/26',
                bulan: 'Februari',
                sumber_energi: 2139,

                konsumsi_listrik: '131.000 VA',
            },
            {
                id: 10,
                nama_tambak: 'Tambak j',
                tanggal: '2022/02/29',
                bulan: 'Februaru',
                sumber_energi: 2323,

                konsumsi_listrik: '131.000 VA',
            },
        ];
    };

    const view_row = (item) => {
        new window.Swal({
            title: '<i>Manage Energi</i>',
            text: 'HALLO',
            html:
                '<p><b>Nama Tambak</b> : ' +
                item.nama_tambak +
                '</p>' +
                '<p><b>Tanggal</b> : ' +
                item.tanggal +
                '</p>' +
                '<p><b>Bulan</b> : ' +
                item.bulan +
                '</p>' +
                '<p><b>Penggunaan listrik (KwH)</b> : ' +
                item.sumber_energi +
                '</p>' +
                '<p><b>Kategori Konsumsi Listrik</b> : ' +
                item.konsumsi_listrik +
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
            confirmButtonColor: '#1695DC',
            confirmButtonText: '<i class="flaticon-checked-1"></i> Oke',
            confirmButtonAriaLabel: 'Oke',

            padding: '2em',
        });
        // alert(' Name: ' + item.nama + ', MIN: ' + item.min + ', MAX: ' + item.max);
    };
</script>
