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
            class="bg-surface-0 border border-black/10 dark:border-white/20 dark:bg-surface-950 w-full h-[80vh] mt-16 rounded-3xl p-6 flex items-start gap-6 overflow-hidden">
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
                            @click="setSelectedSampleAppsSidebarNav(navItem.title)"
                            class="w-full px-4 py-1 flex items-center gap-1 cursor-pointer text-base rounded-lg transition-all select-none"
                            :class="[{ 'text-muted-color hover:bg-emphasis bg-transparent': selectedSampleAppsSidebarNav !== navItem.title, 'text-primary-contrast bg-primary hover:bg-primary-emphasis': selectedSampleAppsSidebarNav === navItem.title }]">
                            <i :class="navItem.icon"></i>
                            <span class="font-medium leading-8">・</span>
                            <span class="font-medium leading-none">{{ navItem.title }}</span>
                        </div>
                    </div>
                    <Divider />
                    <div class="flex items-center gap-3">
                        <Avatar label="V" size="large" style="background-color: #ece9fc; color: #2a1261"
                            shape="circle" />
                        <div>
                            <div class="text-base font-medium text-color leading-5">Robin Jonas</div>
                            <div class="text-sm text-muted-color mt-1">hi@robin.xyz</div>
                        </div>
                    </div>
                </div>
            </div>
            <Overview v-if="selectedSampleAppsSidebarNav === 'Overview'" />
            <Chat v-if="selectedSampleAppsSidebarNav === 'Chat'" />
        </div>
    </section>
</template>

<script>
import EventBus from '@/layouts/AppEventBus';
import { NodeService } from '@/service/NodeService';
import Divider from '@/components/lib/divider/Divider.vue';
import Avatar from '@/components/lib/avatar/Avatar.vue';
import Overview from './app-samples/Overview.vue';
import Chat from './app-samples/Chat.vue';

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
            dates: [],
            selectedTime: 'Monthly',
            timeOptions: ['Monthly', 'Weekly', 'Yearly'],
            sampleAppsTableDatas: [
                {
                    id: '#1254',
                    name: {
                        text: 'Amy Yelsner',
                        label: 'AY',
                        color: 'blue'
                    },
                    coin: 'btc',
                    date: 'May 5th',
                    process: {
                        type: 'success',
                        value: 'Buy'
                    },
                    amount: '3.005 BTC'
                },
                {
                    id: '#2355',
                    name: {
                        text: 'Anna Fali',
                        label: 'AF',
                        color: '#ECFCCB'
                    },
                    coin: 'eth',
                    date: 'Mar 17th',
                    process: {
                        type: 'success',
                        value: 'Buy'
                    },
                    amount: '0.050 ETH'
                },
                {
                    id: '#1235',
                    name: {
                        text: 'Stepen Shaw',
                        label: 'SS',
                        color: '#ECFCCB'
                    },
                    coin: 'btc',
                    date: 'May 24th',
                    process: {
                        type: 'danger',
                        value: 'Sell'
                    },
                    amount: '3.050 BTC'
                },
                {
                    id: '#2355',
                    name: {
                        text: 'Anna Fali',
                        label: 'AF',
                        color: '#ECFCCB'
                    },
                    coin: 'eth',
                    date: 'Mar 17th',
                    process: {
                        type: 'danger',
                        value: 'Sell'
                    },
                    amount: '0.050 ETH'
                },
                {
                    id: '#2355',
                    name: {
                        text: 'Anna Fali',
                        label: 'AF',
                        color: '#ECFCCB'
                    },
                    coin: 'eth',
                    date: 'Mar 17th',
                    process: {
                        type: 'danger',
                        value: 'Sell'
                    },
                    amount: '0.050 ETH'
                }
            ],
            metersData: [
                { label: 'BTC', color: '#F59E0B', value: 15, text: '27.215' },
                { label: 'ETH', color: '#717179', value: 5, text: '4.367' },
                { label: 'GBP', color: '#22C55E', value: 25, text: '£ 147.562,32' },
                { label: 'EUR', color: '#84CC16', value: 11, text: '€ 137.457,25' },
                { label: 'USD', color: '#14B8A6', value: 29, text: '$ 133.364,12' },
                { label: 'XAU', color: '#EAB308', value: 29, text: '200 g' }
            ],
        };
    },
    beforeUnmount() {
        EventBus.off('dark-mode-toggle-complete', this.redrawListener);
        EventBus.off('theme-palette-change', this.redrawListener);
    },
    mounted() {
        this.chartData = this.setChartData();
        this.chartOptions = this.setChartOptions();

        this.redrawListener = () => {
            this.chartData = this.setChartData();
            this.chartOptions = this.setChartOptions();
        };

        EventBus.on('dark-mode-toggle-complete', this.redrawListener);
        EventBus.on('theme-palette-change', this.redrawListener);

        NodeService.getTreeNodes().then((data) => (this.nodes = data));
    },
    methods: {
        setCategory(category) {
            this.category = category;
        },
        setChartData() {
            const documentStyle = getComputedStyle(document.documentElement);

            return {
                labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
                datasets: [
                    {
                        type: 'bar',
                        label: 'Personal Wallet',
                        backgroundColor: 'color-mix(in srgb, ' + documentStyle.getPropertyValue('--p-primary-400') + ' 100%, #fff)',
                        data: [40, 100, 150, 40, 160, 80, 210, 280, 170, 50, 120, 60]
                    },
                    {
                        type: 'bar',
                        label: 'Corporate Wallet',
                        backgroundColor: 'color-mix(in srgb, ' + documentStyle.getPropertyValue('--p-primary-300') + ' 100%, transparent)',
                        data: [21, 84, 24, 75, 37, 65, 34, 12, 48, 90, 76, 42]
                    },
                    {
                        type: 'bar',
                        label: 'Investment Wallet',
                        backgroundColor: 'color-mix(in srgb, ' + documentStyle.getPropertyValue('--p-primary-200') + ' 100%, transparent)',
                        data: [41, 52, 24, 74, 23, 21, 32, 12, 48, 90, 76, 42]
                    }
                ]
            };
        },
        setChartOptions() {
            const documentStyle = getComputedStyle(document.documentElement);
            const textColor = documentStyle.getPropertyValue('--p-text-color');
            const textColorSecondary = documentStyle.getPropertyValue('--p-text-color-secondary');
            const surfaceBorder = documentStyle.getPropertyValue('--p-surface-border');

            return {
                maintainAspectRatio: false,
                aspectRatio: 0.8,
                plugins: {
                    tooltips: {
                        mode: 'index',
                        intersect: false
                    },
                    legend: {
                        labels: {
                            color: textColor
                        }
                    }
                },
                scales: {
                    x: {
                        stacked: true,
                        ticks: {
                            color: textColorSecondary
                        },
                        grid: {
                            color: surfaceBorder
                        }
                    },
                    y: {
                        stacked: true,
                        ticks: {
                            color: textColorSecondary
                        },
                        grid: {
                            color: surfaceBorder
                        }
                    }
                }
            };
        },

        /*Sample Apps Methods*/
        setSelectedSampleAppsSidebarNav(title) {
            this.selectedSampleAppsSidebarNav = title;
        },
    },
    components: {
        Divider,
        Avatar,
        Overview,
        Chat
    },
    redrawListener: null
};

</script>
