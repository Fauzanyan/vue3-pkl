<template>
    <div class="layout-px-spacing">
        <teleport to="#breadcrumb">
            <ul class="navbar-nav flex-row">
                <li>
                    <div class="page-header">
                        <nav class="breadcrumb-one" aria-label="breadcrumb">
                            <ol class="breadcrumb">
                                <li class="breadcrumb-item active" aria-current="page"><span>Harga udang</span></li>
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
                                    <h4>Harga Udang</h4>
                                </div>
                            </div>
                        </div>
                        <div class="d-flex flex-row-reverse position-relative">
                            <router-link to="/hargaudang/create" @click="toggleMobileMenu" class="btn mb-2 mx-3 tambah-data">Tambah Data</router-link>
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
                                        <router-link to="/hargaudang/edit" data-bs-toggle="tooltip" title="Edit">
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

    const columns = ref(['no', 'Tanggal_Input', 'Ukuran_Udang', 'Harga_(Rp)', 'actions']);
    const items = ref([]);
    const table_option = ref({
        perPage: 10,
        perPageValues: [5, 10, 20, 50],
        skin: 'table table-hover',
        columnsClasses: { no: 'no text-end ', actions: 'actions text-center', Tanggal_Input: 'text-center', Ukuran_Udang: 'text-end ', 'Harga_(Rp)': 'text-end ' },
        pagination: { nav: 'scroll', chunk: 5 },
        texts: {
            count: 'Showing {from} to {to} of {count}',
            filter: '',
            filterPlaceholder: 'Search...',
            limit: 'Results:',
        },
        sortable: ['Tanggal_Input', 'Ukuran_Udang', 'Harga_(Rp)'],
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
                Tanggal_Input: '2011/04/25',
                Ukuran_Udang: '32 cm',
                'Harga_(Rp)': '70.000',
                Harga: 'Rp.70000',
            },
            {
                id: 2,
                Tanggal_Input: '2011/07/25',
                Ukuran_Udang: '17 cm',
                'Harga_(Rp)': '10.000',
                Harga: 'Rp.10000',
            },
            {
                id: 3,
                Tanggal_Input: '2009/01/12',
                Ukuran_Udang: '86 cm',
                'Harga_(Rp)': '130.000',
                Harga: 'Rp.130000',
            },
            {
                id: 4,
                Tanggal_Input: '2012/03/29',
                Ukuran_Udang: '43 cm',
                'Harga_(Rp)': '70.000',
                Harga: 'Rp.70000',
            },
            {
                id: 5,
                Tanggal_Input: '2008/11/28',
                Ukuran_Udang: '16 cm',
                'Harga_(Rp)': '50.000',
                Harga: 'Rp.50000',
            },
            {
                id: 6,
                Tanggal_Input: '2012/12/02',
                Ukuran_Udang: '37 cm',
                'Harga_(Rp)': '60.000',
                Harga: 'Rp.60000',
            },
            {
                id: 7,
                Tanggal_Input: '2012/08/06',
                Ukuran_Udang: '13 cm',
                'Harga_(Rp)': '20.000',
                Harga: 'Rp.20000',
            },
            {
                id: 8,
                Tanggal_Input: '2010/10/14',
                Ukuran_Udang: '32 cm',
                'Harga_(Rp)': '50.000',
                Harga: 'Rp.50000',
            },
            {
                id: 9,
                Tanggal_Input: '2009/09/15',
                Ukuran_Udang: '20 cm',
                'Harga_(Rp)': '10.000',
                Harga: 'Rp.10000',
            },
            {
                id: 10,
                Tanggal_Input: '2008/12/13',
                Ukuran_Udang: '10 cm',
                'Harga_(Rp)': '30.000',
                Harga: 'Rp.30000',
            },
        ];
    };

    const view_row = (item) => {
        new window.Swal({
            title: '<i>Manage User</i>',
            text: 'HALLO',
            html: `
        <table role="table" border="5" aria-busy="false" aria-colcount="5" class="table table-0  table-bordered" id="__BVID__415">
                                    <tbody role="rowgroup">
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Tanggal Input</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.Tanggal_Input}</td>
                                        </tr>
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Ukuran Udang</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.Ukuran_Udang}</td>
                                        </tr>
                                        <tr v-for="item in table_1" :key="item.name" role="row">
                                            <td aria-colindex="1" role="cell"><b>Harga</b></td>
                                            <td class="titik-dua"><b>:</b></td>
                                            <td aria-colindex="2" role="cell">${item.Harga}</td>
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
