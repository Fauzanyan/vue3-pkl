<template>
    <div class="layout-px-spacing">
        <teleport to="#breadcrumb">
            <ul class="navbar-nav flex-row">
                <li>
                    <div class="page-header">
                        <nav class="breadcrumb-one" aria-label="breadcrumb">
                            <ol class="breadcrumb">
                                <li class="breadcrumb-item active" aria-current="page"><span>Manage Benur</span></li>
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
                                    <h4>Manage Benur</h4>
                                </div>
                            </div>
                        </div>
                        <div class="d-flex flex-row-reverse position-relative">
                            <router-link to="/manage-Benur/create" @click="toggleMobileMenu" class="btn mb-2 mx-3 tambah-data">Tambah Data</router-link>
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
                                        <router-link to="/manage-Benur/edit" data-bs-toggle="tooltip" title="Edit">
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
                                    <div class="px-2">
                                        <a href="/scoring-benur/create" data-bs-toggle="tooltip" title="Scoring">
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
                                                class="feather feather-clipboard"
                                            >
                                                <path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path>
                                                <rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect>
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

    const columns = ref(['no', 'tambak', 'Tanggal_Input', 'Asal_Benur', 'Usia_Benur(Hari)', 'Scoring', 'actions']);
    const items = ref([]);
    const table_option = ref({
        perPage: 10,
        perPageValues: [5, 10, 20, 50],
        skin: 'table table-hover',
        columnsClasses: { no: 'no text-end ', actions: 'actions text-center', Tanggal_Input: 'text-center', 'Usia_Benur(Hari)': 'text-end ', Scoring: 'text-center ' },
        pagination: { nav: 'scroll', chunk: 5 },
        texts: {
            count: 'Showing {from} to {to} of {count}',
            filter: '',
            filterPlaceholder: 'Search...',
            limit: 'Results:',
        },
        sortable: ['tambak', 'Tanggal_Input', 'Id_benur', 'Asal_Benur', 'benur_batch_id', 'Usia_Benur(Hari)', 'Scoring'],
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
                tambak: 'Tambak a',
                Tanggal_Input: '2022/01/25',
                Id_benur: '1',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '1',
                'Usia_Benur(Hari)': '18 ',
                usia_benur: '18',
                Scoring: 'A',
            },
            {
                id: 2,
                tambak: 'Tambak b',
                Tanggal_Input: '2022/02/26',
                Id_benur: '2',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '2',
                'Usia_Benur(Hari)': '20 ',
                usia_benur: '20',
                Scoring: 'B',
            },
            {
                id: 3,
                tambak: 'Tambak c',
                Tanggal_Input: '2022/03/07',
                Id_benur: '3',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '3',
                'Usia_Benur(Hari)': '20 ',
                usia_benur: '20',
                Scoring: 'B',
            },
            {
                id: 4,
                tambak: 'Tambak d',
                Tanggal_Input: '2022/03/28',
                Id_benur: '4',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '4',
                'Usia_Benur(Hari)': '18 ',
                usia_benur: '18',
                Scoring: 'A',
            },
            {
                id: 5,
                tambak: 'Tambak e',
                Tanggal_Input: '2022/04/10',
                Id_benur: '5',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '5',
                'Usia_Benur(Hari)': '20 ',
                usia_benur: '20',
                Scoring: 'C',
            },
            {
                id: 6,
                tambak: 'Tambak f',
                Tanggal_Input: '2022/05/29',
                Id_benur: '6',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '6',
                'Usia_Benur(Hari)': '18 ',
                usia_benur: '18',
                Scoring: 'A',
            },
            {
                id: 7,
                tambak: 'Tambak g',
                Tanggal_Input: '2022/06/23',
                Id_benur: '7',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '7',
                'Usia_Benur(Hari)': '18 ',
                usia_benur: '18',
                Scoring: 'B',
            },
            {
                id: 8,
                tambak: 'Tambak h',
                Tanggal_Input: '2022/07/21',
                Id_benur: '8',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '8',
                'Usia_Benur(Hari)': '20 ',
                usia_benur: '20',
                Scoring: 'B',
            },
            {
                id: 9,
                tambak: 'Tambak i',
                Tanggal_Input: '2022/08/15',
                Id_benur: '9',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '9',
                'Usia_Benur(Hari)': '20 ',
                usia_benur: '20',
                Scoring: 'C',
            },
            {
                id: 10,
                tambak: 'Tambak j',
                Tanggal_Input: '2022/08/15',
                Id_benur: '10',
                Asal_Benur: 'Udang vaname',
                benur_batch_id: '10',
                'Usia_Benur(Hari)': '19 ',
                usia_benur: '19',
                Scoring: 'A',
            },
        ];
    };

    const view_row = (item) => {
        new window.Swal({
            title: '<i>Manage Benur</i>',
            text: 'HALLO',
            html: `
        <table role="table" border="5" aria-busy="false" aria-colcount="5" class="table table-0  table-bordered" id="__BVID__415">
                                    <tbody role="rowgroup">
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Tambak</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.tambak}</td>
                                        </tr>
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Tanggal_Input</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.Tanggal_Input}</td>
                                        </tr>
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Asal Benur(Hari)</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.Asal_Benur}</td>
                                        </tr>
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Benur Batch ID</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.benur_batch_id}</td>
                                        </tr>
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Usia Benur(Hari)</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.usia_benur}</td>
                                        </tr>
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Scoring</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.Scoring}</td>
                                        </tr>
                                       
                                        
                                    </tbody>
            </table>   
            `,
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
            focusConfirm: true,
            confirmButtonColor: '#1695DC',
            confirmButtonText: '<i class="flaticon-checked-1"></i> Oke',
            confirmButtonAriaLabel: 'Oke',
            confirmButtonClass: 'd-none',

            padding: '2em',
        });
        // alert(' Name: ' + item.nama + ', MIN: ' + item.min + ', MAX: ' + item.max);
    };
</script>
