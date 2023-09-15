<script setup>
import {Head, Link} from '@inertiajs/vue3';
import {ref, resolveDirective} from "vue";
import {Vue3Lottie} from 'vue3-lottie'
import BirthdayJSON from '../json/birthday_two.json';
import VueGallery from 'vue-gallery';
import moment from "moment";

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});

const ntime = ref(0);
const counting = ref(true);
const images = ref([
    '/images/bday/DSC00741.JPG',
    '/images/bday/IMG_7696.JPG',
    '/images/bday/48667a41-ab75-42d3-8eeb-380368453192.jpg',
    '/images/bday/PXL_20221024_234638617.MP.jpg'
]);

const images2 = ref([
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
    'https://images.pexels.com/photos/18036725/pexels-photo-18036725/free-photo-of-food-nature-people-woman.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',

])


const index = ref(null);
const mIndex = ref(null);
const first = ref(0);
const second = ref(0);

const time = (date) => {
    const now = new Date();
    const newYear = new Date(date);
    ntime.value = newYear - now;
}
time('2023-09-16 00:00');

const t1 = ref(0);
const t1Status = ref(false);
const time1 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 00:00');
    t1.value = newYear - now;
}

time1();

const t2 = ref(0);
const t2Status = ref(false);
const time2 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 01:00');
    t2.value = newYear - now;
}

time2();

const t3 = ref(0);
const t3Status = ref(false);
const time3 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 02:00');
    t3.value = newYear - now;
}

time3();



const t4 = ref(0);
const t4Status = ref(false);
const time4 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 03:00');
    t4.value = newYear - now;
}

time4();



const t5 = ref(0);
const t5Status = ref(false);
const time5 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 04:00');
    t5.value = newYear - now;
}

time5();



const t6 = ref(0);
const t6Status = ref(false);
const time6 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 05:00');
    t6.value = newYear - now;
}

time6();



const t7 = ref(0);
const t7Status = ref(false);
const time7 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 06:00');
    t7.value = newYear - now;
}

time7();



const t8 = ref(0);
const t8Status = ref(false);
const time8 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 07:00');
    t8.value = newYear - now;
}

time8();



const t9 = ref(0);
const t9Status = ref(false);
const time9 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 08:00');
    t9.value = newYear - now;
}

time9();



const t10 = ref(0);
const t10Status = ref(false);
const time10 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 09:00');
    t10.value = newYear - now;
}

time10();



const t11 = ref(0);
const t11Status = ref(false);
const time11 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 10:00');
    t11.value = newYear - now;
}

time11();



const t12 = ref(0);
const t12Status = ref(false);
const time12 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 11:00');
    t12.value = newYear - now;
}

time12();



const t13 = ref(0);
const t13Status = ref(false);
const time13 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 12:00');
    t13.value = newYear - now;
}

time13();



const t14 = ref(0);
const t14Status = ref(false);
const time14 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 13:00');
    t14.value = newYear - now;
}

time14();



const t15 = ref(0);
const t15Status = ref(false);
const time15 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 14:00');
    t15.value = newYear - now;
}

time15();



const t16 = ref(0);
const t16Status = ref(false);
const time16 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 15:00');
    t16.value = newYear - now;
}

time16();



const t17 = ref(0);
const t17Status = ref(false);
const time17 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 16:00');
    t17.value = newYear - now;
}

time17();



const t18 = ref(0);
const t18Status = ref(false);
const time18 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 17:00');
    t18.value = newYear - now;
}

time18();



const t19 = ref(0);
const t19Status = ref(false);
const time19 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 18:00');
    t19.value = newYear - now;
}

time19();



const t20 = ref(0);
const t20Status = ref(false);
const time20 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 19:00');
    t20.value = newYear - now;
}

time20();



const t21 = ref(0);
const t21Status = ref(false);
const time21 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 20:00');
    t21.value = newYear - now;
}

time21();

const t22 = ref(0);
const t22Status = ref(false);
const time22 = () => {
    const now = new Date();
    const newYear = new Date('2023-09-16 21:00');
    t22.value = newYear - now;
}

time22();
const countdownEnd = () => {
    counting.value = false;
}

const checkDate = (date) => {
    console.log(moment());
    return moment().isAfter(moment(date))
}


</script>

<template>
    <Head title="Birthday"/>

    <div
        class="relative sm:flex sm:justify-center sm:items-center min-h-screen bg-dots-darker bg-center bg-[#5C755E] dark:bg-dots-lighter dark:bg-[#5C755E] selection:bg-red-500 selection:text-white"
        v-if="counting"
    >
        <button class="absolute right-5 top-5 bg-white border-2 p-3 rounded-md text-xs" @click="counting = false">Off</button>
        <vue-countdown :time="ntime" v-slot="{ days, hours, minutes, seconds }" @end="countdownEnd"
                       class="text-white font-bold text-7xl">
            {{ days }} days, {{ hours }} hours, {{ minutes }} minutes, {{ seconds }} seconds.
        </vue-countdown>
    </div>
    <div v-else class="">
        <div
            class="dark:bg-dots-lighter dark:bg-[#5C755E] relative w-full min-h-screen flex flex-col items-center justify-center">
            <video src="/videos/bg/Happy.mp4" muted loop autoplay class="absolute top-0 left-0 w-full h-full object-cover"></video>
<!--            <div class="absolute top-0 left-0 w-full h-full bg-gradient-to-l from-indigo-500 via-purple-500 to-pink-500 mix-blend-overlay"></div>-->
<!--            <vue3-lottie :animation-data="BirthdayJSON" :width="600" :height="500"/>-->
<!--            <h3 class="text-white font-bold text-7xl bg-pink-700 mt-3 absolute bottom-10">Happy Birthday SNEJANA</h3>-->
        </div>
<!--        <div class="mt-5 flex items-center justify-center">-->
<!--            <vue-gallery-->
<!--                :images="images"-->
<!--                :index="index"-->
<!--                :id="'gallery-123'"-->
<!--                @close="index = null"-->
<!--            />-->
<!--            <div-->
<!--                class="image cursor-pointer"-->
<!--                v-for="(image, imageIndex) in images"-->
<!--                :key="imageIndex"-->
<!--                @click="index = imageIndex"-->
<!--                :style="{ backgroundImage: 'url(' + image + ')', width: '300px', height: '200px' }"-->
<!--            ></div>-->
<!--        </div>-->

        <div class="mt-10 flex flex-col items-center justify-center font-bold text-4xl md:text-2xl">
            <h2>Birthday Wishes.</h2>

            <div class="mt-5 flex flex-wrap items-center justify-center">
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px] outline-0"
                       src="/videos/wishes/4035250d-0560-413f-a711-5f9b2910d0ac.MP4"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px]"
                       src="/videos/wishes/IMG_4880.MOV"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px]"
                       src="/videos/wishes/IMG_4881.MOV"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px]"
                       src="/videos/wishes/IMG_4883.MOV"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px]"
                       src="/videos/wishes/IMG_4884.MOV"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px]"
                       src="/videos/wishes/IMG_4885.MOV"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px]"
                       src="/videos/wishes/VIDEO-2023-09-13-12-57-57.mp4"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
               <div class="flex flex-col mr-3 mb-6 items-center">
                   <video
                       class="w-[350px] h-[300px]"
                       src="/videos/wishes/VIDEO-2023-09-13-14-50-05.mp4"
                       width="350px" height="300px" controls>
                   </video>
<!--                   <p class="text-xl font-semibold text-gray-500">John Doe</p>-->
               </div>
            </div>
        </div>

        <div class="banner">
            <div class="mt-5 flex flex-wrap items-center justify-center">
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/48667a41-ab75-42d3-8eeb-380368453192.jpg" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t1Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t1" v-slot="{ days, hours, minutes, seconds }" @end="t1Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t1Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/DSC00741.JPG" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t2Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t2" v-slot="{ days, hours, minutes, seconds }" @end="t2Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t2Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_2173.JPG" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t3Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t3" v-slot="{ days, hours, minutes, seconds }" @end="t3Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t3Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_7297.JPG" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t4Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t4" v-slot="{ days, hours, minutes, seconds }" @end="t4Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t4Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_7696.JPG" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t5Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t5" v-slot="{ days, hours, minutes, seconds }" @end="t5Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t5Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_8314.JPG" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t6Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t6" v-slot="{ days, hours, minutes, seconds }" @end="t6Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t6Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/PXL_20221024_234638617.MP.jpg" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t7Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t7" v-slot="{ days, hours, minutes, seconds }" @end="t7Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t7Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_2374-ANIMATION.gif" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t8Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t8" v-slot="{ days, hours, minutes, seconds }" @end="t8Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t8Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_1030.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t9Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t9" v-slot="{ days, hours, minutes, seconds }" @end="t9Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t9Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_1054.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t10Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t10" v-slot="{ days, hours, minutes, seconds }" @end="t10Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t10Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_1104.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t11Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t11" v-slot="{ days, hours, minutes, seconds }" @end="t11Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t11Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_1245.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t12Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t12" v-slot="{ days, hours, minutes, seconds }" @end="t12Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t12Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_1507.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t13Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t13" v-slot="{ days, hours, minutes, seconds }" @end="t13Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t13Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_2522.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t14Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t14" v-slot="{ days, hours, minutes, seconds }" @end="t14Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t14Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_3038.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t15Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t15" v-slot="{ days, hours, minutes, seconds }" @end="t15Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t15Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_4007.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t16Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t16" v-slot="{ days, hours, minutes, seconds }" @end="t16Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t16Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_4747.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t17Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t17" v-slot="{ days, hours, minutes, seconds }" @end="t17Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t17Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_7716.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t18Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t18" v-slot="{ days, hours, minutes, seconds }" @end="t18Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t18Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_9950.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t19Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t19" v-slot="{ days, hours, minutes, seconds }" @end="t19Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t19Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
<!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_1340.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t20Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t20" v-slot="{ days, hours, minutes, seconds }" @end="t20Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t20Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
                        <!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
                <div class="border-4 border-white mb-4 rounded-md flex flex-col items-center justify-center">
                    <div
                        class="relative w-[350px] h-[240px] cursor-pointer"
                    >
                        <img src="/images/bday/IMG_1328.HEIC" class="absolute w-full h-full bg-center object-cover" alt="">
                        <div
                            v-if="t21Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex flex-col items-center justify-center">
                            <i class="fa fa-lock text-white text-3xl mb-14 mt-14 inline-block"></i>
                            <vue-countdown :time="t21" v-slot="{ days, hours, minutes, seconds }" @end="t21Status = true"
                                           class="text-white font-bold text-3xl">
                                {{ hours }} : {{ minutes}} : {{ seconds}}
                            </vue-countdown>
                        </div>
                    </div>
                    <h3 class="max-w-[350px] relative text-center"
                        style=""
                    >
                        <div
                            v-if="t21Status === false"
                            class="bg-black opacity-95 absolute w-full h-full flex items-center justify-center"></div>
                        <!--                        Lorem ipsum dolor sit amet, consectetur adipisicing elit. Blanditiis fugiat quo sint voluptatem! Aliquid aperiam beatae dolorem facilis impedit ipsum, itaque laboriosam magnam, nobis perferendis recusandae reiciendis rerum sequi totam.-->
                    </h3>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
.banner {
    position: relative;
    width: 100%;
    min-height: 100vh;
    display: flex;
    //justify-content: center;
    align-items: center;
    background: url(/images/annie-spratt-0ZPSX_mQ3xI-unsplash.jpg);
    background-size: cover;
}

.banner:last-child {
    margin-bottom: 200px;
}
.bg-dots-darker {
    background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(0,0,0,0.07)'/%3E%3C/svg%3E");
}

@media (prefers-color-scheme: dark) {
    .dark\:bg-dots-lighter {
        background-image: url("data:image/svg+xml,%3Csvg width='30' height='30' viewBox='0 0 30 30' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M1.22676 0C1.91374 0 2.45351 0.539773 2.45351 1.22676C2.45351 1.91374 1.91374 2.45351 1.22676 2.45351C0.539773 2.45351 0 1.91374 0 1.22676C0 0.539773 0.539773 0 1.22676 0Z' fill='rgba(255,255,255,0.07)'/%3E%3C/svg%3E");
    }
}

.image {
    float: left;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    border: 1px solid #ebebeb;
    margin: 5px;
}

.trailer {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 10000;
    background: rgba(0, 0, 0, 0.95);
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    visibility: hidden;
    opacity: 0;
}

.trailer.active {
    visibility: visible;
    opacity: 1;
}

.trailer video {
    max-width: 900px;
    outline: none;
}
</style>
