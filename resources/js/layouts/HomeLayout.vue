<script setup lang="ts">
import { login, register } from '@/routes';
import { index as adminCarsIndex } from '@/routes/admin/cars/index';
import { index as clientReservationsIndex } from '@/routes/client/reservations/index';
import { Link } from '@inertiajs/vue3';
import { usePage } from '@inertiajs/vue3';
import { home } from '@/routes';
import { fleet } from '@/routes';
import { about } from '@/routes';
import { contact } from '@/routes';

const $page = usePage();

const role = $page.props.auth.user?.role;

const dashboardLink = role === 'admin' ? adminCarsIndex() : clientReservationsIndex();
</script>

<template>
    <div>
        <header
    class="sticky top-0 z-50 border-b border-gray-100 bg-white/95 shadow-sm backdrop-blur-md"
>
    <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <nav class="flex h-16 items-center justify-between">
            <div class="flex items-center space-x-2">
               <img src="/logo/logi.png" alt="logo" style="width: 90px; height: 65px;">
                <p class="font-bold">
                    RAP<span class="text-blue-500">REN</span>TAL
                </p>
            </div>


                    <div class="hidden items-center space-x-8 md:flex">
                        <Link 
                            :href="home()" 
                            :class="{ 'text-blue-500': $page.url === home().url, 'text-gray-700': $page.url !== home().url }" 
                            class="font-medium transition-colors hover:text-blue-500"
                        >
                            Beranda
                        </Link>
                        <Link 
                            :href="fleet()" 
                            :class="{ 'text-blue-500': $page.url.startsWith('/fleet'), 'text-gray-700': !$page.url.startsWith('/fleet') }" 
                            class="font-medium transition-colors hover:text-blue-500"
                        >
                            Armada
                        </Link>
                        <Link 
                            :href="about()" 
                            :class="{ 'text-blue-500': $page.url === '/about', 'text-gray-700': $page.url !== '/about' }" 
                            class="font-medium transition-colors hover:text-blue-500"
                        >
                            Tentang Kami
                        </Link>
                        <Link 
                            :href="contact()" 
                            :class="{ 'text-blue-500': $page.url === '/contact', 'text-gray-700': $page.url !== '/contact' }" 
                            class="font-medium transition-colors hover:text-blue-500"
                        >
                            Kontak
                        </Link>
                    </div>

                    <div class="flex items-center space-x-3">
                        <Link
                            v-if="$page.props.auth.user"
                            :href="dashboardLink"
                            class="inline-flex items-center rounded-xl bg-gray-50 px-6 py-2.5 text-sm font-semibold text-gray-700 transition-all duration-200 hover:bg-gray-100 hover:shadow-md"
                        >
                            <svg
                                class="mr-2 h-4 w-4"
                                fill="none"
                                stroke="currentColor"
                                viewBox="0 0 24 24"
                            >
                                <path
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                    stroke-width="2"
                                    d="M4 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2V6zM14 6a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2V6zM4 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2H6a2 2 0 01-2-2v-2zM14 16a2 2 0 012-2h2a2 2 0 012 2v2a2 2 0 01-2 2h-2a2 2 0 01-2-2v-2z"
                                ></path>
                            </svg>
                            Dasbor
                        </Link>
                        <template v-else>
                            <Link
                                :href="login()"
                                class="inline-flex items-center px-6 py-2.5 text-sm font-semibold text-gray-700 transition-colors duration-200 hover:text-blue-600"
                            >
                                Masuk
                            </Link>
                            <Link
                                :href="register()"
                                class="inline-flex items-center rounded-xl bg-gradient-to-r from-blue-500 to-blue-600 px-6 py-2.5 text-sm font-semibold text-white shadow-lg transition-all duration-200 hover:scale-105 hover:from-blue-600 hover:to-blue-700 hover:shadow-xl"
                            >
                                Mulai Sekarang
                            </Link>
                        </template>
                    </div>
                </nav>
            </div>
        </header>

        <slot />

        <footer class="bg-gray-900 py-16 text-white">
            <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
                <div class="grid gap-12 md:grid-cols-4">
                    <div class="space-y-6">
                        <div class="flex items-center space-x-2">
                            <div
                                class="flex h-10 w-10 items-center justify-center rounded-xl bg-gradient-to-br from-blue-500 to-blue-600"
                            >
                                <svg
                                    class="h-6 w-6 text-white"
                                    fill="none"
                                    stroke="currentColor"
                                    viewBox="0 0 24 24"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M13 10V3L4 14h7v7l9-11h-7z"
                                    ></path>
                                </svg>
                            </div>
                            <div>
                                <h3 class="text-xl font-bold">
                                    Rap<span class="text-blue-500"
                                        >RENTAL</span
                                    >
                                </h3>
                                <p class="text-xs font-medium text-gray-400">
                                    MOBIL PREMIUM
                                </p>
                            </div>
                        </div>
                        <p class="leading-relaxed text-gray-400">
                            Layanan sewa mobil premium yang menyediakan kendaraan
                            mewah dan terpercaya untuk semua kebutuhan
                            transportasi Anda dengan layanan pelanggan yang luar biasa.
                        </p>
                    </div>

                    <div class="space-y-6">
                        <h4 class="text-lg font-semibold">Layanan</h4>
                        <ul class="space-y-3 text-gray-400">
                            <li>
                                <a
                                    href="#"
                                    class="transition-colors hover:text-blue-500"
                                    >Sewa Cepat</a
                                >
                            </li>
                            <li>
                                <a
                                    href="#"
                                    class="transition-colors hover:text-blue-500"
                                    >Sewa Jangka Panjang</a
                                >
                            </li>
                            <li>
                                <a
                                    href="#"
                                    class="transition-colors hover:text-blue-500"
                                    >Solusi Korporat</a
                                >
                            </li>
                            <li>
                                <a
                                    href="#"
                                    class="transition-colors hover:text-blue-500"
                                    >Transfer Bandara</a
                                >
                            </li>
                        </ul>
                    </div>

                    <div class="space-y-6">
                        <h4 class="text-lg font-semibold">Bantuan</h4>
                        <ul class="space-y-3 text-gray-400">
                            <li>
                                <a
                                    :href="contact.url()"
                                    class="transition-colors hover:text-blue-500"
                                    >Kontak Kami</a
                                >
                            </li>
                            <li>
                                <a
                                    href="#"
                                    class="transition-colors hover:text-blue-500"
                                    >Pusat Bantuan</a
                                >
                            </li>
                            <li>
                                <a
                                    href="#"
                                    class="transition-colors hover:text-blue-500"
                                    >Syarat & Ketentuan</a
                                >
                            </li>
                            <li>
                                <a
                                    href="#"
                                    class="transition-colors hover:text-blue-500"
                                    >Kebijakan Privasi</a
                                >
                            </li>
                        </ul>
                    </div>

                    <div class="space-y-6">
                        <h4 class="text-lg font-semibold">Info Kontak</h4>
                        <div class="space-y-3 text-gray-400">
                            <div class="flex items-center space-x-3">
                                <svg
                                    class="h-5 w-5 text-blue-500"
                                    fill="none"
                                    stroke="currentColor"
                                    viewBox="0 0 24 24"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
                                    ></path>
                                </svg>
                                <span>+62 857-1377-2932</span>
                            </div>
                            <div class="flex items-center space-x-3">
                                <svg
                                    class="h-5 w-5 text-blue-500"
                                    fill="none"
                                    stroke="currentColor"
                                    viewBox="0 0 24 24"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M3 8l7.89 4.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"
                                    ></path>
                                </svg>
                                <span>RapRental@gmail.com</span>
                            </div>
                            <div class="flex items-center space-x-3">
                                <svg
                                    class="h-5 w-5 text-blue-500"
                                    fill="none"
                                    stroke="currentColor"
                                    viewBox="0 0 24 24"
                                >
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                                    ></path>
                                    <path
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="2"
                                        d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                                    ></path>
                                </svg>
                                <span>JL.Pentul, Kota Semarang</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="mt-2 border-t border-gray-800 pt-8">
                    <p class="text-gray-400 text-center">
                        &copy; 2025 RapRental. Semua hak dilindungi.
                    </p>
                </div>
            </div>
        </footer>
    </div>
</template>