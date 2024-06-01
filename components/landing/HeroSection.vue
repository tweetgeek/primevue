<template>
    <section class="landing-hero py-20 px-8 lg:px-20">
        <div class="flex flex-col items-center">
            <h1 class="text-5xl font-bold text-center xl:text-left leading-tight">The Next-Gen UI Suite for <span class="font-bold text-primary">Vue.js</span></h1>
            <p class="text-center mt-0 mb-8 text-surface-500 dark:text-surface-400 font-medium text-xl leading-relaxed">
                Enhance your web applications with PrimeVue's comprehensive suite of customizable, feature-rich UI components. With PrimeVue, turning your development vision into reality has never been easier.
            </p>
            <div class="flex items-center gap-4">
                <PrimeVueNuxtLink to="/setup" class="linkbox linkbox-primary">
                    <span>Get Started</span>
                    <i class="pi pi-arrow-right ml-4"></i>
                </PrimeVueNuxtLink>
                <a href="https://github.com/primefaces/primevue" target="_blank" rel="noopener noreferrer" class="linkbox">
                    <span>Give a Star</span>
                    <i class="pi pi-star-fill ml-4 text-yellow-500"></i>
                </a>
            </div>
        </div>
        <div class="bg-surface-50 dark:bg-surface-950">Dashboard</div>
    </section>
</template>

<script>
import EventBus from '@/layouts/AppEventBus';
import { NodeService } from '@/service/NodeService';

export default {
    redrawListener: null,
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
            ]
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
            const primaryColor = documentStyle.getPropertyValue('--primary-color');

            return {
                labels: ['Q1', 'Q2', 'Q3', 'Q4'],
                datasets: [
                    {
                        label: 'Annual Income',
                        data: [40, 59, 40, 50, 56],
                        fill: true,
                        borderColor: primaryColor,
                        tension: 0.4,
                        backgroundColor: `color-mix(in srgb, ${primaryColor}, transparent 80%)`
                    }
                ]
            };
        },
        setChartOptions() {
            const documentStyle = getComputedStyle(document.documentElement);
            const textColorSecondary = documentStyle.getPropertyValue('--p-text-muted-color');
            const surfaceBorder = documentStyle.getPropertyValue('p-content-border-color');

            return {
                plugins: {
                    legend: {
                        display: false
                    }
                },
                scales: {
                    x: {
                        ticks: {
                            color: textColorSecondary
                        },
                        grid: {
                            color: surfaceBorder
                        }
                    },
                    y: {
                        beginAtZero: true,
                        ticks: {
                            color: textColorSecondary
                        },
                        min: 0,
                        max: 100,
                        grid: {
                            color: surfaceBorder
                        }
                    }
                }
            };
        }
    }
};
</script>
