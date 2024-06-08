<template>
    <section class="landing-hero py-20 px-8 lg:px-20">
        <div class="flex flex-col items-center">
            <h1 class="text-5xl font-bold text-center xl:text-left leading-tight">The Next-Gen UI Suite for <span
                    class="font-bold text-primary">Vue.js</span></h1>
            <p class="text-center mt-0 mb-8 text-surface-500 dark:text-surface-400 font-medium text-xl leading-relaxed">
                Enhance your web applications with PrimeVue's comprehensive suite of customizable, feature-rich UI
                components. With PrimeVue, turning your development vision into reality has never been easier.
            </p>
            <div class="flex items-center gap-4">
                <PrimeVueNuxtLink to="/setup" class="linkbox linkbox-primary">
                    <span>Get Started</span>
                    <i class="pi pi-arrow-right ml-4"></i>
                </PrimeVueNuxtLink>
                <a href="https://github.com/primefaces/primevue" target="_blank" rel="noopener noreferrer"
                    class="linkbox">
                    <span>Give a Star</span>
                    <i class="pi pi-star-fill ml-4 text-yellow-500"></i>
                </a>
            </div>
        </div>
        <div
            class="bg-surface-0 border border-black/10 dark:border-white/20 dark:bg-surface-950 w-full h-[85vh] mt-16 rounded-3xl p-6 flex items-start gap-6 overflow-hidden">
            <div class="w-72 rounded-2xl p-5 bg-surface-50 dark:bg-surface-900 h-full flex flex-col justify-between">
                <div>
                    <div class="flex items-center gap-3">
                        <div class="w-11 h-11">
                            <img class="w-full h-auto" src="/demo/images/logo.png" alt="Logo" />
                        </div>
                        <div class="text-surface-950 dark:text-surface-0 font-medium text-3xl">Aura</div>
                    </div>
                    <div class="mt-10 flex flex-col gap-2">
                        <div v-for="(navItem, index) in sampleAppsSidebarNavs" :key="index"
                            @click="setSelectedSampleAppsSidebarNav(navItem.title)"
                            class="w-full px-4 py-1 flex items-center gap-1 cursor-pointer text-base rounded-lg transition-all select-none"
                            :class="[{ 'text-muted-color hover:bg-emphasis bg-transparent': selectedSampleAppsSidebarNav !== navItem.title, 'text-primary-contrast bg-primary hover:bg-primary-emphasis': selectedSampleAppsSidebarNav === navItem.title }]">
                            <i :class="navItem.icon"></i>
                            <span class="font-medium leading-8">・</span>
                            <span class="font-medium leading-none">{{ navItem.title }}</span>
                        </div>
                    </div>
                </div>
                <div>
                    <div class="mt-10 flex flex-col gap-2">
                        <div v-for="(navItem, index) in sampleAppsSidebarNavsMore" :key="index"
                            class="w-full px-4 py-1 flex items-center gap-1 cursor-pointer text-base rounded-lg transition-all select-none"
                            :class="[{ 'text-muted-color hover:bg-emphasis bg-transparent': selectedSampleAppsSidebarNav !== navItem.title, 'text-primary-contrast bg-primary hover:bg-primary-emphasis': selectedSampleAppsSidebarNav === navItem.title }]">
                            <i :class="navItem.icon"></i>
                            <span class="font-medium leading-8">・</span>
                            <span class="font-medium leading-none">{{ navItem.title }}</span>
                        </div>
                    </div>
                    <Divider />
                    <div class="flex items-center gap-3">
                        <Avatar image="/demo/images/main-avatar.png" size="large" shape="circle" />
                        <div>
                            <div class="text-base font-medium text-color leading-5">Robin Jonas</div>
                            <div class="text-sm text-muted-color mt-1">hi@robin.xyz</div>
                        </div>
                    </div>
                </div>
            </div>
            <Overview v-if="selectedSampleAppsSidebarNav === 'Overview'" />
            <Chat v-if="selectedSampleAppsSidebarNav === 'Chat'" />
            <Movies v-if="selectedSampleAppsSidebarNav === 'Movies'" />
            <Cards v-if="selectedSampleAppsSidebarNav === 'Cards'" />
            <Inbox v-if="selectedSampleAppsSidebarNav === 'Inbox'" />
            <Customers v-if="selectedSampleAppsSidebarNav === 'Customers'" />
        </div>
    </section>
</template>

<script>
import Avatar from '@/components/lib/avatar/Avatar.vue';
import Divider from '@/components/lib/divider/Divider.vue';
import EventBus from '@/layouts/AppEventBus';
import { NodeService } from '@/service/NodeService';
import Cards from './app-samples/Cards.vue';
import Chat from './app-samples/Chat.vue';
import Customers from './app-samples/Customers.vue';
import Inbox from './app-samples/Inbox.vue';
import Movies from './app-samples/Movies.vue';
import Overview from './app-samples/Overview.vue';
export default {
    data() {
        return {
            value1: 24,
            category: 'C',
            chartData: {},
            chartOptions: {},
            pbValue1: 15,
            pbValue2: 85,
            pbValue3: 50,
            pbValue4: 75,
            pbValue5: 60,
            activeTabIndex: 0,
            radioValue: 'S',
            nodes: null,
            switchValue: true,
            selectButtonValue: { name: 'Styled', value: 1 },
            dateValue: null,
            rangeValues: [20, 80],
            checked: false,
            splitButtonItems: [
                {
                    label: 'Update',
                    icon: 'pi pi-refresh'
                },
                {
                    label: 'Delete',
                    icon: 'pi pi-times'
                }
            ],
            items: [
                { label: 'Home', icon: 'pi pi-fw pi-home' },
                { label: 'Inbox', icon: 'pi pi-fw pi-inbox' }
            ],
            selectButtonOptions: [
                { name: 'Styled', value: 1 },
                { name: 'Unstyled', value: 2 }
            ],
            user: null,
            users: [
                { name: 'Amy Elsner', image: 'amyelsner.png' },
                { name: 'Bernardo Dominic', image: 'bernardodominic.png' },
                { name: 'Onyama Limba', image: 'onyamalimba.png' }
            ],
            /*Sample Apps Data*/
            sampleAppsSidebarNavs: [
                { icon: 'pi pi-home', title: 'Overview' },
                { icon: 'pi pi-comment', title: 'Chat' },
                { icon: 'pi pi-inbox', title: 'Inbox' },
                { icon: 'pi pi-th-large', title: 'Cards' },
                { icon: 'pi pi-user', title: 'Customers' },
                { icon: 'pi pi-video', title: 'Movies' },
            ],
            sampleAppsSidebarNavsMore: [
                { icon: 'pi pi-flag', title: 'Support' },
                { icon: 'pi pi-cog', title: 'Settings' },
            ],
            selectedSampleAppsSidebarNav: 'Overview',

        };
    },
    beforeUnmount() {
        EventBus.off('dark-mode-toggle-complete', this.redrawListener);
        EventBus.off('theme-palette-change', this.redrawListener);
    },
    mounted() {
        EventBus.on('dark-mode-toggle-complete', this.redrawListener);
        EventBus.on('theme-palette-change', this.redrawListener);

        NodeService.getTreeNodes().then((data) => (this.nodes = data));
    },
    methods: {
        setCategory(category) {
            this.category = category;
        },
        setSelectedSampleAppsSidebarNav(title) {
            this.selectedSampleAppsSidebarNav = title;
        },
    },
    components: {
        Divider,
        Avatar,
        Overview,
        Chat,
        Movies,
        Cards,
        Inbox,
        Customers
    },
    redrawListener: null
};

</script>
