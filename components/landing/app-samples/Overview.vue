<template>
    <div class="flex-1 h-full overflow-y-auto overflow-x-clip">
        <div class="flex flex-wrap gap-4 items-start justify-between">
            <div class="flex-1">
                <div class="text-muted-color font-medium leading-normal">Overview</div>
                <div class="text-color text-3xl font-semibold leading-normal">Good Morning, Robin 👋</div>
            </div>
            <div class="flex gap-2 whitespace-nowrap flex-nowrap">
                <IconField iconPosition="left">
                    <InputIcon class="pi pi-search"> </InputIcon>
                    <InputText placeholder="Search" />
                </IconField>
                <button
                    class="bg-transparent text-color border-surface rounded-border hover:bg-emphasis cursor-pointer border px-2.5 transition-all">
                    <OverlayBadge severity="danger">
                        <i class="pi pi-bell" />
                    </OverlayBadge>
                </button>
            </div>
        </div>
        <div class="mt-4 flex flex-wrap gap-6 items-start justify-between">
            <SelectButton v-model="selectedTime" :options="timeOptions" aria-labelledby="basic" />
            <div class="flex items-center gap-2">
                <Button label="Download" icon="pi pi-download" iconPos="right" />
                <Calendar v-model="dates" selectionMode="range" :manualInput="false" showIcon iconDisplay="input" />
            </div>
        </div>

        <div class="flex flex-col gap-6 mt-6">

            <div class="w-full border border-surface rounded-2xl py-5 px-7 flex flex-col justify-between">
                <div class="flex items-center gap-6 mb-6">
                    <div class="flex-1 text-color font-semibold leading-6">Crypto Analytics</div>
                    <Button icon="pi pi-ellipsis-h" severity="secondary" text aria-label="Bookmark" />
                </div>
                <Chart type="bar" :data="chartData" :options="chartOptions" class="h-72" />
            </div>
            <div class="flex gap-6">
                <div class="flex-1 border border-surface rounded-2xl py-5 px-7">
                    <div class="flex items-center gap-6 mb-4">
                        <div class="flex-1 text-color font-semibold leading-6">Transactions</div>
                        <Button icon="pi pi-ellipsis-h" severity="secondary" text aria-label="Bookmark" />
                    </div>
                    <DataTable :value="sampleAppsTableDatas" paginator :rows="5" dataKey="id"
                        tableClass="overflow-x-auto dark:bg-surface-950" :rowsPerPageOptions="[5, 10, 20, 50]"
                        paginatorTemplate="RowsPerPageDropdown PrevPageLink CurrentPageReport NextPageLink" :pt="{
                            bodyrow: {
                                class: 'bg-transparent'
                            }
                        }">
                        <Column header="Id" class="w-1/12">
                            <template #body="slotProps">
                                <div class="text-muted-color">{{ slotProps.data.id }}</div>
                            </template>
                        </Column>
                        <Column header="Name" class="w-1/4">
                            <template #body="slotProps">
                                <div class="flex items-center">
                                    <Avatar :label="slotProps.data.name.label" class="mr-2 text-xs font-medium"
                                        style="background-color: #ece9fc; color: #2a1261" shape="circle" />
                                    <div class="leading-6 text-muted-color">{{ slotProps.data.name.text }}</div>
                                </div>
                            </template>
                        </Column>
                        <Column header="Coin" class="w-1/6">
                            <template #body="slotProps">
                                <div class="flex items-center">
                                    <i
                                        :class="[{ 'pi pi-bitcoin text-yellow-500 text-3xl': slotProps.data.coin !== 'btc', 'pi pi-ethereum bg-surface-950 text-surface-0 dark:bg-surface-0 dark:text-surface-950 w-7 h-7 rounded-full flex items-center justify-center': slotProps.data.coin !== 'eth' }]"></i>
                                </div>
                            </template>
                        </Column>
                        <Column header="Date" class="w-1/6">
                            <template #body="slotProps">
                                <div class="text-muted-color">{{ slotProps.data.date }}</div>
                            </template>
                        </Column>
                        <Column header="Process" class="w-1/6">
                            <template #body="slotProps">
                                <Tag :severity="slotProps.data.process.type" :value="slotProps.data.process.value">
                                </Tag>
                            </template>
                        </Column>
                        <Column header="Amount" class="w-1/6">
                            <template #body="slotProps">
                                <div class="text-muted-color text-right">{{ slotProps.data.amount }}</div>
                            </template>
                        </Column>
                    </DataTable>
                </div>
                <div class="w-96 border border-surface rounded-2xl py-5 px-7 flex flex-col justify-between">
                    <div>
                        <div class="flex items-center gap-6 mb-6">
                            <div class="flex-1 text-color font-semibold leading-6">My Wallet</div>
                            <Button icon="pi pi-ellipsis-h" severity="secondary" text aria-label="Bookmark" />
                        </div>
                        <MeterGroup :value="metersData" labelPosition="end">
                            <template #label="{ value }">
                                <div class="flex flex-col gap-6 mt-4">
                                    <template v-for="val of value" :key="val.label">
                                        <div class="flex items-center gap-2">
                                            <div class="w-2 h-2 rounded-full" :style="{ backgroundColor: val.color }">
                                            </div>
                                            <div class="text-color uppercase font-medium leading-6 flex-1">{{
                                                val.label }}
                                                <span class="text-muted-color">({{
                                                    val.value }}%)</span>
                                            </div>
                                            <div class="leading-6 font-medium text-color">{{ val.text }}</div>
                                        </div>
                                    </template>
                                </div>
                            </template>
                        </MeterGroup>
                    </div>
                    <Button label="Show All" outlined />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Avatar from '@/components/lib/avatar/Avatar.vue';
import IconField from '@/components/lib/iconfield/IconField.vue'
import InputIcon from '@/components/lib/inputicon/InputIcon.vue'
import InputText from '@/components/lib/inputtext/InputText.vue'
import OverlayBadge from '@/components/lib/overlaybadge/OverlayBadge.vue'
import MeterGroup from '@/components/lib/metergroup/MeterGroup.vue'
import Column from '@/components/lib/column/Column.vue'
import DataTable from '@/components/lib/datatable/DataTable.vue'
import Chart from '@/components/lib/chart/Chart.vue'
import Button from '@/components/lib/button/Button.vue'
import Calendar from '@/components/lib/calendar/Calendar.vue'
import SelectButton from '@/components/lib/selectbutton/SelectButton.vue'
export default {
    name: 'Overview',
    redrawListener: null,
    data() {
        return {
            chartData: {},
            chartOptions: {},
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
    mounted() {
        this.chartData = this.setChartData();
        this.chartOptions = this.setChartOptions();
    },
    methods: {
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
        }
    },
    components: {
        Avatar,
        IconField,
        InputIcon,
        InputText,
        OverlayBadge,
        MeterGroup,
        Column,
        DataTable,
        Chart,
        Button,
        SelectButton,
        Calendar
    },
};

</script>
