<script setup lang="ts">
import HomeLayout from '@/layouts/HomeLayout.vue';
import { useForm } from '@inertiajs/vue3';
import { guestContact } from "@/routes/contact";
import { ref } from 'vue';
import { fleet } from '@/routes';
import { about } from '@/routes';

const form = useForm({
    name: '',
    email: '',
    subject: '',
    message: '',
});

const showNotification = ref(false);
const notificationMessage = ref('');

const sendTicket = () => {
    form.post(guestContact().url, {
        onSuccess() {
            form.reset();
            showNotification.value = true;
            notificationMessage.value = 'Message sent successfully!';
            setTimeout(() => {
                showNotification.value = false;
            }, 2000);
        },
        onError() {
            showNotification.value = true;
            notificationMessage.value = 'Failed to send message! Please try again.';
            setTimeout(() => {
                showNotification.value = false;
            }, 2000);
        }
    });
}
</script>
<template>
    <HomeLayout>
        <div class="min-h-screen bg-white py-16 ">
            <!-- notification -->
            <div>
                <p class="fixed top-24 right-4 bg-slate-700 text-white p-3 rounded-xl" v-if="showNotification">{{ notificationMessage }}</p>
            </div>
            <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
                <!-- Header Section -->
                <div class="mb-16 text-center">
                    <h1 class="mb-4 text-4xl font-bold text-gray-900">
                        Kontak Kami
                    </h1>
                    <p class="mx-auto max-w-2xl text-xl text-gray-600">
                        Punya pertanyaan tentang layanan sewa mobil kami? Kami siap membantu. 
                        Kirimkan pesan kepada kami dan kami akan membalas secepat mungkin.
                    </p>
                </div>

                <div class="grid gap-12 lg:grid-cols-3">
                    <!-- Contact Form -->
                    <div class="lg:col-span-2">
                        <div
                            class="rounded-lg border border-gray-200 bg-white p-8 shadow-sm"
                        >
                            <h2 class="mb-6 text-2xl font-bold text-gray-900">
                                Panduan Mengisi Formulir Kontak
                            </h2>

                            <form class="space-y-6"
                            
                            @submit.prevent="sendTicket">
                                <!-- Name Field -->
                                <div>
                                    <label
                                        for="name"
                                        class="mb-2 block text-sm font-semibold text-gray-700"
                                    >
                                        Nama Lengkap
                                    </label>
                                    <input
                                        type="text"
                                        id="name"
                                        name="name"
                                        class="w-full rounded-lg border border-gray-300 px-4 py-3 transition-colors focus:border-orange-500 focus:ring-2 focus:ring-orange-500"
                                        placeholder="Masukan Nama Lengkap Anda"
                                        v-model="form.name"
                                    />
                                    <span class="text-red-500" v-if="form.errors.name">{{ form.errors.name }}</span>
                                </div>

                                <!-- Email Field -->
                                <div>
                                    <label
                                        for="email"
                                        class="mb-2 block text-sm font-semibold text-gray-700"
                                    >
                                        Email
                                    </label>
                                    <input
                                        type="email"
                                        id="email"
                                        name="email"
                                        class="w-full rounded-lg border border-gray-300 px-4 py-3 transition-colors focus:border-orange-500 focus:ring-2 focus:ring-orange-500"
                                        placeholder="Masukan Alamat Email Anda"
                                        v-model="form.email"
                                    />
                                    <span class="text-red-500" v-if="form.errors.email">{{ form.errors.email }}</span>
                                </div>

                                <!-- Subject Field -->
                                <div>
                                    <label
                                        for="subject"
                                        class="mb-2 block text-sm font-semibold text-gray-700"
                                    >
                                        No Telepon
                                    </label>
                                    <input
                                        type="text"
                                        id="subject"
                                        name="subject"
                                        class="w-full rounded-lg border border-gray-300 px-4 py-3 transition-colors focus:border-orange-500 focus:ring-2 focus:ring-orange-500"
                                        placeholder="+62"
                                        v-model="form.subject"
                                    />
                                    <span class="text-red-500" v-if="form.errors.subject">{{ form.errors.subject }}</span>
                                </div>

                                <!-- Message Field -->
                                <div>
                                    <label
                                        for="message"
                                        class="mb-2 block text-sm font-semibold text-gray-700"
                                    >
                                        Pesan
                                    </label>
                                    <textarea
                                        id="message"
                                        name="message"
                                        rows="6"
                                        class="resize-vertical w-full rounded-lg border border-gray-300 px-4 py-3 transition-colors focus:border-orange-500 focus:ring-2 focus:ring-orange-500"
                                        placeholder="Beri tahu kami apa yang anda perlukan"
                                        v-model="form.message"
                                    ></textarea>
                                    <span class="text-red-500" v-if="form.errors.message">{{ form.errors.message }}</span>
                                </div>

                                <!-- Submit Button -->
                                <div>
                                    <button
                                        type="submit"
                                        class="w-full cursor-pointer rounded-lg bg-orange-500 px-6 py-3 font-semibold text-white transition-colors duration-200 hover:bg-orange-600"
                                    >
                                        Kirim
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>

                    <!-- Contact Information Sidebar -->
                    <div class="lg:col-span-1">
                        <div
                            class="rounded-lg border border-gray-200 bg-gray-50 p-8"
                        >
                            <h3 class="mb-6 text-xl font-bold text-gray-900">
                                Kirim pesan kepada kami
                            </h3>

                            <div class="space-y-6">
                                <!-- Phone -->
                                <div>
                                    <h4
                                        class="mb-2 font-semibold text-gray-900"
                                    >
                                        No telepon
                                    </h4>
                                    <p class="text-gray-600">
                                        +62 857-1377-2932
                                    </p>
                                </div>

                                <!-- Email -->
                                <div>
                                    <h4
                                        class="mb-2 font-semibold text-gray-900"
                                    >
                                        Email
                                    </h4>
                                    <p class="text-gray-600">
                                        RAP@gmail.com
                                    </p>
                                </div>

                                <!-- Address -->
                                <div>
                                    <h4
                                        class="mb-2 font-semibold text-gray-900"
                                    >
                                        Alamat
                                    </h4>
                                    <p class="text-gray-600">
                                        JL.Pentul raya<br />
                                        Kelurahan Bendan Duwur<br />
                                        Kota, Semarang 50932
                                    </p>
                                </div>

                                <!-- Business Hours -->
                                <div>
                                    <h4
                                        class="mb-2 font-semibold text-gray-900"
                                    >
                                        Jam Kerja
                                    </h4>
                                    <div class="space-y-1 text-gray-600">
                                        <p>
                                            Senin - Jumat: 8:00 AM - 8:00 PM
                                        </p>
                                        <p>Sabtu: 08:00 AM - 6:00 PM</p>
                                        <p>Minggu: 08:00 AM - 4:00 PM</p>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Quick Links -->
                        <div
                            class="mt-8 rounded-lg border border-gray-200 bg-white p-6"
                        >
                            <h3 class="mb-4 text-lg font-bold text-gray-900">
                                Quick Links
                            </h3>
                            <div class="space-y-3">
                                <a
                                    :href="fleet.url()"
                                    class="block font-medium text-orange-500 transition-colors hover:text-orange-600"
                                >
                                    Cari Kendaraan Anda
                                </a>
                                <a
                                    :href="about.url()"
                                    class="block font-medium text-orange-500 transition-colors hover:text-orange-600"
                                >
                                    Tentang Kami
                                </a>
                                
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </HomeLayout>
</template>
