<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">riwayat kunjungan</h2>
                <div class="my-3">
                    <input type="search" class="form-control rounded-5" placeholder="Fiter...">
                </div>
                 <div class="my-3 text-muted">menampilkan 1 drat</div>
                 <table class="table">
                    <thead>
                        <tr>
                            <td>#</td>
                            <td>NAMA</td>
                            <td>KEANGGOTAAN</td>
                            <td>WAKTU</td>
                            <td>KEPERLUAN</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>1.</td>
                            <td>Zul Hilmi</td>
                            <td>Guru</td>
                            <td>24 februari 2024, 23.31.00</td>
                            <td>Baca</td>
                        </tr>
                    </tbody>
                 </table>
            </div>
        </div>
        <NuxtLink to="/pengunjung/tambah">
            <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">kembali</button>
        </NuxtLink>
    </div>
</template>