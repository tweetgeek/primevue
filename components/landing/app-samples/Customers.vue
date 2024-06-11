<template>
    <div class="h-full flex-1 flex flex-col overflow-hidden border border-surface rounded-2xl p-6">
        <div class="flex items-start gap-2 justify-between">
            <div>
                <div class="text-2xl leading-8 text-color font-medium">Customers</div>
                <div class="mt-1 leading-6 text-muted-color">The analysis list here shows all users</div>
            </div>
            <Button icon="pi pi-circle-fill text-green-500" label="950 Active User" outlined severity="secondary" />
        </div>
        <div class="mt-10 mb-4 flex items-center justify-between">
            <IconField iconPosition="left">
                <InputIcon class="pi pi-search"> </InputIcon>
                <InputText v-model="value1" placeholder="Search" />
            </IconField>
            <div class="flex items-center gap-3">
                <Button icon="pi pi-filter" outlined severity="secondary" />
                <Divider layout="vertical" class="m-0" />
                <Button icon="pi pi-refresh" outlined severity="secondary" />
                <Button label="1 of 15" outlined severity="secondary" />
                <Button icon="pi pi-chevron-left" outlined severity="secondary" />
                <Button icon="pi pi-chevron-right" outlined severity="secondary" />
            </div>
        </div>
        <div class="flex-1 last:[&>td]:border-0 rounded-lg border border-surface w-full overflow-auto">
            <DataTable v-model:selection="selectedRows" selectionMode="multiple" :value="tableData" :rows="10" :pt="{
                root: {
                    class: 'w-full flex-1 overflow-auto '
                },
                thead: {
                    class: 'sticky top-0 z-10'
                },
            }">
                <template #empty>There is no customer.</template>
                <Column selectionMode="multiple" headerStyle="width: 1rem" style="width: 1rem"></Column>
                <Column field="name" header="Name">
                    <template #body="{ data }">
                        <div class="flex items-center">
                            <OverlayBadge
                                :severity="data.active === undefined ? 'contrast' : data.active ? 'success' : 'danger'"
                                class="w-fit">
                                <Avatar v-bind="data.image ? { image: data.image } : { label: data.capName }" :class="{
                                    'bg-violet-100 text-violet-950 text-xs font-medium': !data.image
                                }" class="rounded-md overflow-hidden flex" />
                            </OverlayBadge>
                            <div class="ml-4 leading-6 text-color font-medium">{{ data.name }}</div>
                        </div>
                    </template>
                </Column>
                <Column field="title" header="Title">
                    <template #body="{ data }">
                        <div class="leading-6 text-muted-color">{{ data.title }}</div>
                    </template>
                </Column>
                <Column field="company" header="Company Name">
                    <template #body="{ data }">
                        <div class="flex items-center gap-2">
                            <img :src="data.company.logo" />
                            <div class="leading-6 text-surface-600 dark:text-surface-400">{{ data.company.name }}</div>
                        </div>
                    </template>
                </Column>
                <Column field="email" header="Email Address">
                    <template #body="{ data }">
                        <div class="leading-6 text-muted-color truncate">{{ data.email }}</div>
                    </template>
                </Column>
                <Column field="lead" header="Lead Source">
                    <template #body="{ data }">
                        <div class="leading-6 text-muted-color">{{ data.lead }}</div>
                    </template>
                </Column>
                <Column field="status" header="Status">
                    <template #body="{ data }">
                        <Tag :severity="data.status === 'Active' ? 'success' : data.status === 'Inactive' ? 'danger' : 'info'"
                            :value="data.status" class="font-medium"></Tag>
                    </template>
                </Column>
                <Column field="more" header="More">
                    <template #body>
                        <div class="flex justify-end w-full">
                            <Button @click="visibleRight = true" icon="pi pi-ellipsis-h" outlined
                                severity="secondary" />
                        </div>
                    </template>
                </Column>
            </DataTable>
        </div>
    </div>
    <Sidebar v-model:visible="visibleRight" :containerVisible="true" header="Right Sidebar" position="right"
        closeIcon="pi pi-sign-out" :pt="{
            root: {
                class: '!max-w-2xl !w-full !h-[100vh] rounded-l-2xl'
            },
            footer: {
                class: 'hidden'
            },
            content: {
                class: 'flex-1 flex flex-col'
            }
        }">
        <template #container="">
            <div class="flex flex-col h-[100vh] overflow-auto">
                <div class="">
                    <div class="flex align-items-center gap-3 p-6">
                        <Avatar image="/demo/images/avatar11.jpg" size="large" class="rounded-xl overflow-hidden" />
                        <div class="flex-1">
                            <div class="leading-6 text-color font-medium">Brook Simmons</div>
                            <div class="mt-1 leading-5 text-muted-color text-sm">Sales Executive </div>
                        </div>
                        <Button icon="pi pi-sign-out" text rounded severity="secondary" />
                    </div>
                    <SelectButton v-model="selectedSidebarOption" :options="sidebarOptions" :pt="{
                        root: {
                            class: 'px-6 py-3 w-full'
                        },
                        pcButton: {
                            root: {
                                class: 'flex-1 py-2.5'
                            },
                            label: {
                                class: 'text-sm'
                            }
                        }

                    }" />
                </div>
                <div v-if="selectedSidebarOption === 'Interaction Logs'"
                    class="h-[calc(100%-172px)] flex flex-col gap-4 p-6">
                    <div class="h-1/3 flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="flex items-start justify-between">
                            <div class="leading-6 font-medium text-color">Call Logs</div>
                            <Button icon="pi pi-download text-sm"
                                class="w-8 h-8 !border-surface !bg-surface-0 dark:!bg-surface-900 hover:opacity-75 transition-all"
                                severity="secondary" text />
                        </div>
                        <div
                            class="overflow-y-auto flex-1 bg-surface-0 dark:bg-surface-900 mt-2 flex flex-col rounded-lg overflow-hidden divide-y divide-surface-200 dark:divide-surface-800">
                            <div v-for="(data, index) of callLogs" :key="index" class="flex items-center gap-3 p-2">
                                <OverlayBadge severity="success" class="w-fit">
                                    <Avatar :image="data.image" size="small"
                                        class="rounded-md w-10 h-10 overflow-hidden flex" />
                                </OverlayBadge>

                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color">{{ data.name }}</div>
                                    <div class="mt-1 text-sm leading-5 text-muted-color">{{ data.time }}</div>
                                </div>
                                <Button icon="pi pi-phone text-sm" text
                                    class="bg-primary/10 dark:bg-primary/20 w-8 h-8" />
                            </div>
                        </div>
                    </div>
                    <div class="h-1/3 flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="flex items-start justify-between">
                            <div class="leading-6 font-medium text-color">Email Records</div>
                            <Button icon="pi pi-download text-sm"
                                class="w-8 h-8 !border-surface !bg-surface-0 dark:!bg-surface-900 hover:opacity-75 transition-all"
                                severity="secondary" text />
                        </div>
                        <div
                            class="overflow-y-auto flex-1 bg-surface-0 dark:bg-surface-900 mt-2 flex flex-col rounded-lg overflow-hidden divide-y divide-surface-200 dark:divide-surface-800">
                            <div v-for="(data, index) of emailRecords" :key="index" class="flex items-center gap-3 p-2">
                                <OverlayBadge severity="danger" class="w-fit">
                                    <Avatar :image="data.image" size="small"
                                        class="rounded-md overflow-hidden w-10 h-10 flex" />
                                </OverlayBadge>
                                <div class="w-1/5 text-sm leading-5 font-medium text-color">{{ data.name }}</div>
                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color line-clamp-2">
                                        {{ data.title }}
                                        <span class="text-muted-color ">
                                            {{ data.text }}
                                        </span>
                                    </div>
                                </div>
                                <div class="w-1/6 text-sm leading-5 text-muted-color text-right">{{ data.time }} </div>
                            </div>
                        </div>
                    </div>
                    <div class="h-1/3 flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="flex items-start justify-between">
                            <div class="leading-6 font-medium text-color">Meeting Notes</div>
                            <Button icon="pi pi-download text-sm"
                                class="w-8 h-8 !border-surface !bg-surface-0 dark:!bg-surface-900 hover:opacity-75 transition-all"
                                severity="secondary" text />
                        </div>
                        <div
                            class="overflow-y-auto flex-1 bg-surface-0 dark:bg-surface-900 mt-2 p-4 flex flex-col rounded-lg overflow-hidden ">
                            <div class="flex items-start justify-between gap-1">
                                <div class="text-sm text-color font-medium max-w-60">Subject: Meeting Wrap-up & Action
                                    Items:
                                    Jacob
                                    Jones
                                </div>
                                <div class="text-sm text-muted-color">February 14, 2024 / 2:00 PM</div>
                            </div>
                            <div class="text-sm text-muted-color mt-6">
                                Here's a quick review of our meeting with Brook Simmons and next steps. Summary:
                                <br />
                                <ul class="list-disc pl-5">
                                    <li>Reviewed our SaaS solution and its features.</li>
                                    <li>Arlene McCoy intrigued by user experience potential.</li>
                                    <li>Voiced concerns on integration with current system.Action Items:</li>
                                </ul>
                                Demo: Schedule product demo with Arlene McCoy. (Assigned to: Jerome Bell)<br /><br />
                                Integration Blueprint: Draft and deliver technical blueprint. (Assigned to: Cameron
                                Williamson)<br /><br />
                                Follow-up Meeting: Arrange to discuss any queries post-demo. (Assigned to: Dianne
                                Russell)
                                <br /><br />
                                Please act on these items promptly.
                            </div>
                        </div>
                    </div>
                </div>
                <div v-if="selectedSidebarOption === 'Preferences'" class="h-[calc(100%-72px)] flex flex-col gap-4 p-6">
                    <div v-for="(data, i) of preferences" :key="i"
                        class="h-1/4 flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="leading-6 font-medium text-color p-2">{{ data.title }}</div>
                        <div
                            class="overflow-y-auto flex-1 bg-surface-0 dark:bg-surface-900 mt-2 p-4 flex flex-col gap-3 rounded-lg">
                            <div v-for="(pref, j) of data.prefs" :key="j" class="flex items-center gap-2">
                                <i class="text-lg text-color" :class="pref.icon"></i>
                                <div class="font-medium text-color flex-1">{{ pref.title }}</div>
                                <InputSwitch v-model="pref.checked" />
                            </div>
                        </div>
                    </div>
                </div>
                <div v-if="selectedSidebarOption === 'Opportunities'" class="grid grid-cols-2 gap-6 p-6">
                    <div v-for="(data, i) of opportunities" :key="i" class="flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="flex items-start justify-between gap-2">
                            <div class="font-medium text-color mt-0.5">{{ data.title }}</div>
                            <NuxtLink :to="data.link" target="_blank" rel="noopener">
                                <Button icon="pi pi-arrow-up-right text-sm"
                                    class="w-8 h-8 !border-surface !bg-surface-0 dark:!bg-surface-900"
                                    severity="secondary" text />
                            </NuxtLink>
                        </div>
                        <img class="w-full rounded-lg mt-2 block" :src="data.image" alt="Opportunutiy Image" />
                        <div class="flex-1 mt-2 p-2 rounded-lg bg-surface-0 dark:bg-surface-900 text-xs text-color">
                            {{ data.text }}
                        </div>
                    </div>
                </div>
                <div v-if="selectedSidebarOption === 'Statistics'" class="h-[calc(100%-160px)] p-6">
                    <div class="grid grid-cols-2 gap-4">
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="flex items-center justify-between gap-2">
                                <div class="font-medium text-color p-2">Customer Satisfaction Score</div>
                            </div>
                            <div
                                class="flex-1 py-4 mt-2 flex items-center justify-center rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                                <Knob v-model="customerSatisfaction" :size="150" :strokeWidth="8"
                                    valueTemplate="{value}%" />
                            </div>
                        </div>
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="flex items-center justify-between gap-2">
                                <div class="font-medium text-color p-2">Estimated Lifetime Value</div>
                            </div>
                            <div
                                class="flex-1 flex items-center gap-2 justify-center mt-2 p-2 rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                                <div
                                    class="font-semibold text-lg leading-none text-color border border-surface py-3.5 px-2 rounded-lg">
                                    $</div>
                                <div
                                    class="font-semibold text-lg leading-none text-color border border-surface py-3.5 px-2 rounded-lg">
                                    272</div>
                                <div
                                    class="font-semibold text-lg leading-none text-color border border-surface py-3.5 px-2 rounded-lg">
                                    123</div>
                                <div
                                    class="font-semibold text-lg leading-none text-color border border-surface py-3.5 px-2 rounded-lg">
                                    000</div>
                            </div>
                        </div>
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="flex items-center justify-between gap-2">
                                <div class="font-medium text-color p-2">Product Usage</div>
                            </div>
                            <div class="flex-1 mt-2 py-4 rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                                <Chart type="line" :data="lineChartData" :options="lineChartOptions"
                                    class="min-h-44 w-full" />
                            </div>
                        </div>
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="font-medium text-color p-2">Churn Risk</div>
                            <div
                                class="flex-1 py-4 mt-2 flex items-center justify-center rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                                <Knob v-model="customerSatisfaction" :size="150" :strokeWidth="8"
                                    valueTemplate="{value}%" />
                            </div>
                        </div>
                    </div>
                    <div class="mt-4 w-full flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="font-medium text-color p-2">Churn Risk</div>
                        <div
                            class="flex-1 py-4 px-2 w-full mt-2 flex items-center justify-center rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                            <Chart type="bar" :data="chartData" :options="chartOptions" class="h-60 w-full" />
                        </div>
                    </div>
                </div>
            </div>
        </template>
    </Sidebar>
</template>

<script>
import Avatar from '@/components/lib/avatar/Avatar.vue';
import Button from '@/components/lib/button/Button.vue';
import IconField from '@/components/lib/iconfield/IconField.vue';
import InputIcon from '@/components/lib/inputicon/InputIcon.vue';
import InputText from '@/components/lib/inputtext/InputText.vue';
import EventBus from '@/layouts/AppEventBus';
export default {
    name: 'Inbox',
    redrawListener: null,
    data() {
        return {
            lineChartData: {},
            lineChartOptions: {},
            chartData: {},
            chartOptions: {},
            tableData: [
                { id: 1, image: '/demo/images/avatar2.png', active: true, name: 'Brook Simmons', title: 'Sales Executive ', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@brooksmmns.co', lead: 'Linkedin', status: 'Active' },
                { id: 2, image: '/demo/images/avatar9.jpg', active: true, name: 'Dianne Russell', title: 'CEO', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@diannerussell.com', lead: 'Website', status: 'Inactive' },
                { id: 3, image: '/demo/images/avatar13.jpg', active: undefined, name: 'Amy Elsner', title: 'Product Manager', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@amyelsner.com', lead: 'Cold Call', status: 'Prospect' },
                { id: 4, image: '/demo/images/avatar11.jpg', active: true, name: 'Jacob Jones', title: 'Manager', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'jacobjones@gmail.com', lead: 'Partner', status: 'Prospect' },
                { id: 5, image: '', active: false, name: 'Cameron Watson', capName: 'CW', title: 'Product Manager', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@cameronwilliamson', lead: 'Social Media', status: 'Active' },
                { id: 6, image: '', active: true, name: 'Wade Warren', capName: 'WW', title: 'Director', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@annetteblack.com', lead: 'Cold Call', status: 'Inactive' },
                { id: 7, image: '/demo/images/avatar7.png', active: true, name: 'Guy Hawkins', title: 'Director', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@darrellsteward.com', lead: 'Linkedin', status: 'Active' },
                { id: 8, image: '/demo/images/avatar8.png', active: true, name: 'Annette Black', title: 'Manager', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'jeromebell@gmail.com', lead: 'Website', status: 'Inactive' },
                { id: 9, image: '/demo/images/avatar10.jpg', active: undefined, name: 'Darrell Steward', title: 'Product Manager', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@onyamalimba.co', lead: 'Website', status: 'Active' },
                { id: 10, image: '', active: true, name: 'Jerome Bell', capName: 'JB', title: 'Marketing Manager', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@courtneyhenryo', lead: 'Social Media', status: 'Active' },
                { id: 11, image: '/demo/images/avatar12.jpg', active: undefined, name: 'Onyama Limba', title: 'Sales Executive ', company: { name: 'Mistranet', logo: '/demo/images/mistranet.svg' }, email: 'hi@arlenemccoy.com', lead: 'Social Media', status: 'Active' },
            ],
            selectedRows: [],
            visibleRight: false,
            selectedSidebarOption: 'Statistics',
            sidebarOptions: ['Interaction Logs', 'Preferences', 'Statistics', 'Opportunities'],
            callLogs: [
                { image: '/demo/images/avatar6.png', name: 'Brook Simmons', time: '02.02.2024 | 45 min' },
                { image: '/demo/images/avatar12.jpg', name: 'Jacob Jones', time: '02.02.2024 | 45 min' },
                { image: '/demo/images/avatar13.jpg', name: 'Annette Black', time: '02.03.2024 | 13 min' },
                { image: '/demo/images/avatar9.jpg', name: 'Arlene McCoy', time: '02.03.2024 | 14 min' },
                { image: '/demo/images/avatar10.jpg', name: 'Arlene Simmons', time: '02.03.2024 | 14 min' },
                { image: '/demo/images/avatar11.jpg', name: 'Michael Brown', time: '02.04.2024 | 20 min' }
            ],
            emailRecords: [
                { image: '/demo/images/avatar2.png', name: 'Brook Simmons', time: '3:24 PM', title: 'Unleash Business Potential', text: "Automate, analyze, and accelerate with our SaaS platform. Unshackle from mundane tasks and focus on scaling your business. Contact us for a demo today!" },
                { image: '/demo/images/avatar7.png', name: 'Jacob Jones', time: '12.23.2023', title: 'Optimized Workflow Revolution  ', text: "Experience a workflow revolution with our intuitive SaaS tool. With enhanced features and optimized processes, it's efficiency like never before. Let's get in touch for a brief demo!" },
                { image: '/demo/images/avatar8.png', name: 'Annette Black', time: '12.17.2023', title: 'Innovation at Fingertips', text: "With our SaaS solution, innovation is only a click away. Shape your future with pioneering features and minimalist design. Join us for your solution walk-through today!" },
                { image: '/demo/images/avatar11.jpg', name: 'Arlene McCoy', time: '06.17.2023', title: 'Seamless Integration', text: "Integrate effortlessly with our user-friendly SaaS tools. Streamline your operations and boost productivity. Discover more in our demo session." },
                { image: '/demo/images/avatar13.jpg', name: 'Arlene Simmons', time: '04.17.2023', title: 'Transform Your Business', text: "Empower your team with our innovative SaaS solutions. Achieve unparalleled efficiency and drive growth. Book a demo to explore the possibilities." },
                { image: '/demo/images/avatar2.png', name: 'Michael Brown', time: '01.05.2024', title: 'Next-Gen Collaboration', text: 'Experience the future of collaboration with our cutting-edge SaaS platform. Enhance teamwork and streamline communication. Contact us for a demo today!' }

            ],
            preferences: [
                {
                    title: 'Email',
                    prefs: [
                        { icon: 'pi pi-bell', title: 'Notification', checked: true },
                        { icon: 'pi pi-inbox', title: 'Newsletter', checked: false },
                        { icon: 'pi pi-sync', title: 'Product Updates', checked: false },
                    ]
                },
                {
                    title: 'Telephone',
                    prefs: [
                        { icon: 'pi pi-mobile', title: 'Phone Call', checked: true },
                        { icon: 'pi pi-volume-down', title: 'Voicemail', checked: false },
                        { icon: 'pi pi-comments', title: 'SMS text', checked: false },
                    ]
                },
                {
                    title: 'Social Media',
                    prefs: [
                        { icon: 'pi pi-clock', title: 'Automated Post', checked: true },
                        { icon: 'pi pi-user', title: 'Direct Message', checked: false },
                    ]
                },
                {
                    title: 'Data Privacy',
                    prefs: [
                        { icon: 'pi pi-box', title: 'Share Data with 3rd Parties', checked: true },
                        { icon: 'pi pi-file', title: 'Cookies', checked: false },
                    ]
                },
            ],
            opportunities: [
                { title: 'Apollo', link: 'https://primevue.org/templates/apollo/', image: 'https://primefaces.org/cdn/primevue/images/layouts/apollo-vue.jpg', text: "Keep your application fresh with Apollo, the newest and most modern template available." },
                { title: 'Ultima', link: 'https://primevue.org/templates/ultima/', image: 'https://primefaces.org/cdn/primevue/images/layouts/ultima-vue.jpg', text: "Elevate your application's intuitiveness with Ultima's premium Material Design interface." },
                { title: 'Diamond', link: 'https://primevue.org/templates/diamond/', image: 'https://primefaces.org/cdn/primevue/images/layouts/diamond-vue.jpg', text: "Handle complex operations with elegance with Diamond's robust and powerful premium design." },
                { title: 'Atlantis', link: 'https://primevue.org/templates/atlantis/', image: 'https://primefaces.org/cdn/primevue/images/layouts/atlantis-vue.jpg', text: "Boost your application's capabilities, customization with the Atlantis template." },
                { title: 'Verona', link: 'https://primevue.org/templates/verona/', image: 'https://primefaces.org/cdn/primevue/images/layouts/verona-vue.jpg', text: "Achieve sophistication and subtlety with Verona's minimalistic, content-focused design." },
                { title: 'Freya', link: 'https://primevue.org/templates/freya/', image: 'https://primefaces.org/cdn/primevue/images/layouts/freya-vue.png', text: "Give your application a sleek, updated look with Freya's chic and modern premium template." },
            ],
            customerSatisfaction: 56,
            churnRisk: 24,
        };
    },
    beforeUnmount() {
        EventBus.off('dark-mode-toggle-complete', this.redrawListener);
        EventBus.off('theme-palette-change', this.redrawListener);
    },
    mounted() {
        this.chartData = this.setChartData();
        this.chartOptions = this.setChartOptions();
        this.lineChartData = this.setLineChartData();
        this.lineChartOptions = this.setLineChartOptions();

        this.redrawListener = () => {
            this.chartOptions = this.setChartOptions();
            this.chartData = this.setChartData();
            this.lineChartData = this.setLineChartData();
            this.lineChartOptions = this.setLineChartOptions();
        };

        EventBus.on('theme-palette-change', this.redrawListener);
        EventBus.on('dark-mode-toggle-complete', this.redrawListener);
    },
    methods: {
        toggle(event) {
            this.$refs.menu.toggle(event);
        },
        setChartData() {
            const documentStyle = getComputedStyle(document.documentElement);
            const darkMode = document.documentElement.classList.contains('p-dark');

            return {
                labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
                datasets: [
                    {
                        type: 'bar',
                        label: 'Investment Wallet',
                        backgroundColor: 'color-mix(in srgb, ' + documentStyle.getPropertyValue(darkMode ? '--p-surface-700' : '--p-surface-200') + ' 100%, transparent)',
                        data: [100, 201, 404, 300, 140, 220, 314, 520, 145, 234, 325, 147],
                        borderRadius: {
                            topLeft: 4,
                            topRight: 4
                        },
                        borderSkipped: true,
                        barThickness: 16,
                        hoverBackgroundColor: 'color-mix(in srgb, ' + documentStyle.getPropertyValue(darkMode ? '--p-surface-0' : '--p-surface-800') + ' 100%, transparent)',
                        hoverTransition: '1s ease all'
                    }
                ]
            };
        },
        setChartOptions() {
            const darkMode = document.documentElement.classList.contains('p-dark');
            const documentStyle = getComputedStyle(document.documentElement);

            const backgroundColor = documentStyle.getPropertyValue(darkMode ? '--p-surface-900' : '--p-surface-0');
            const textColor = documentStyle.getPropertyValue('--p-text-color');
            const borderColor = documentStyle.getPropertyValue(darkMode ? '--p-surface-800' : '--p-surface-100');
            const textMutedColor = documentStyle.getPropertyValue(darkMode ? '--p-surface-500' : '--p-surface-400');

            const getOrCreateTooltip = (chart) => {
                let tooltipEl = chart.canvas.parentNode.querySelector('div.chartjs-tooltip');

                if (!tooltipEl) {
                    tooltipEl = document.createElement('div');
                    tooltipEl.classList.add('chartjs-tooltip');
                    tooltipEl.style.backgroundColor = backgroundColor
                    tooltipEl.style.boxShadow = ' 0px 33.12px 9.399px 0px rgba(0, 0, 0, 0.00), 0px 21.036px 8.504px 0px rgba(0, 0, 0, 0.01), 0px 12.084px 7.161px 0px rgba(0, 0, 0, 0.05), 0px 5.371px 5.371px 0px rgba(0, 0, 0, 0.09), 0px 1.343px 2.685px 0px rgba(0, 0, 0, 0.10)'
                    tooltipEl.style.borderRadius = '7px';
                    tooltipEl.style.color = textColor;
                    tooltipEl.style.opacity = 1;
                    tooltipEl.style.padding = '14.5px'
                    tooltipEl.style.pointerEvents = 'none';
                    tooltipEl.style.position = 'absolute';
                    tooltipEl.style.transform = 'translate(-50%, 0)';
                    tooltipEl.style.transition = 'all .2s ease';
                    chart.canvas.parentNode.appendChild(tooltipEl);
                }

                return tooltipEl;
            };

            return {
                maintainAspectRatio: false,
                aspectRatio: 0.8,
                plugins: {
                    chartAreaBorder: {
                        borderColor: 'red',
                        borderWidth: 2,
                        borderDash: [5, 5],
                        borderDashOffset: 2,
                    },
                    tooltip: {
                        enabled: false,
                        padding: 5,
                        position: 'nearest',
                        external: function (context) {
                            // Tooltip Element
                            const { chart, tooltip } = context;
                            const tooltipEl = getOrCreateTooltip(chart);

                            // Hide if no tooltip
                            if (tooltip.opacity === 0) {
                                tooltipEl.style.opacity = 0;

                                return;
                            }

                            if (tooltip.body) {
                                const bodyLines = tooltip.body.map(b => {
                                    const strArr = b.lines[0].split(':');
                                    const data = {
                                        text: strArr[0].trim(),
                                        value: strArr[1].trim()
                                    }

                                    return data;
                                });

                                // Clear old content
                                tooltipEl.innerHTML = '';
                                bodyLines.forEach((body, i) => {

                                    const text = document.createElement('div');

                                    text.appendChild(document.createTextNode('$' + body.value + 'K'))
                                    text.style.fontWeight = '500'
                                    text.style.lineHeight = '21px'
                                    text.style.fontSize = '14px'
                                    tooltipEl.appendChild(text);
                                });


                            }

                            const { offsetLeft: positionX, offsetTop: positionY } = chart.canvas;

                            // Display, position, and set styles for font
                            tooltipEl.style.opacity = 1;
                            tooltipEl.style.left = positionX + tooltip.caretX + 'px';
                            tooltipEl.style.top = positionY + tooltip.caretY + 'px';
                            tooltipEl.style.font = tooltip.options.bodyFont.string;
                            tooltipEl.style.padding = tooltip.options.padding + 'px ' + tooltip.options.padding + 'px';
                        }
                    },
                    legend: {
                        display: false,
                    }
                },
                scales: {
                    x: {
                        stacked: true,
                        ticks: {
                            color: textMutedColor,
                            font: {
                                weight: 'lighter'
                            }
                        },
                        grid: {
                            color: 'transparent',
                            borderColor: 'transparent'
                        }
                    },
                    y: {
                        border: {
                            display: false,
                        },
                        stacked: true,
                        ticks: {
                            color: textMutedColor,
                            font: {
                                weight: 'lighter'
                            }
                        },
                        grid: {
                            color: borderColor,
                            borderColor: 'transparent'
                        }
                    }
                }
            };
        },
        setLineChartData() {
            const darkMode = document.documentElement.classList.contains('p-dark');

            return {
                labels: ['31', '1', '2', '3', '4', '5', '6', '7', '8'],
                datasets: [{
                    label: 'My First Dataset',
                    data: [60, 64, 57, 52, 58, 70, 75, 70, 60],
                    fill: true,
                    borderColor: '#16A34A',
                    tension: 0.4,
                    borderWidth: 1.5,
                    pointBackgroundColor: "#16A34A",
                    pointBorderColor: darkMode ? "#09090B" : "#FFF",
                    pointBorderWidth: 3,

                    hideInLegendAndTooltip: false,
                    pointStyle: function (context) {
                        let index = context.dataIndex;

                        if (index == 6) {
                            return 'circle';
                        } else {
                            return 'line';
                        }

                    },
                    pointRadius: function (context) {
                        let index = context.dataIndex;

                        if (index == 6) {
                            return 6;
                        } else {
                            return 0.1;
                        }
                    },
                    backgroundColor: (context) => {
                        const bgColor = [
                            'rgba(22,163,74,0.16)',
                            'rgba(22,163,74,0)',
                        ]

                        if (!context.chart.chartArea) {
                            return;
                        }

                        const { ctx, data, chartArea: { top, bottom } } = context.chart;
                        const gradientBg = ctx.createLinearGradient(0, top, 0, bottom);
                        const colorTranches = 1 / (bgColor.length - 1);

                        for (let i = 0; i < bgColor.length; i++) {
                            gradientBg.addColorStop(0 + i * colorTranches, bgColor[i])
                        }

                        return gradientBg;
                    }
                }],
                options: {
                    responsive: true,
                    plugins: {
                        legend: {
                            position: 'top',
                        },
                        title: {
                            display: true,
                            text: 'Chart.js Line Chart'
                        }
                    }
                },
            }
        },
        setLineChartOptions() {
            const darkMode = document.documentElement.classList.contains('p-dark');
            const documentStyle = getComputedStyle(document.documentElement);

            const backgroundColor = documentStyle.getPropertyValue(darkMode ? '--p-surface-900' : '--p-surface-0');
            const textColor = documentStyle.getPropertyValue('--p-text-color');
            const borderColor = documentStyle.getPropertyValue(darkMode ? '--p-surface-800' : '--p-surface-100');
            const textMutedColor = documentStyle.getPropertyValue(darkMode ? '--p-surface-500' : '--p-surface-400');

            const getOrCreateTooltip = (chart) => {
                let tooltipEl = chart.canvas.parentNode.querySelector('div.chartjs-tooltip');

                if (!tooltipEl) {
                    tooltipEl = document.createElement('div');
                    tooltipEl.classList.add('chartjs-tooltip');
                    tooltipEl.style.backgroundColor = backgroundColor
                    tooltipEl.style.boxShadow = ' 0px 33.12px 9.399px 0px rgba(0, 0, 0, 0.00), 0px 21.036px 8.504px 0px rgba(0, 0, 0, 0.01), 0px 12.084px 7.161px 0px rgba(0, 0, 0, 0.05), 0px 5.371px 5.371px 0px rgba(0, 0, 0, 0.09), 0px 1.343px 2.685px 0px rgba(0, 0, 0, 0.10)'
                    tooltipEl.style.borderRadius = '7px';
                    tooltipEl.style.color = textColor;
                    tooltipEl.style.opacity = 1;
                    tooltipEl.style.padding = '2px'
                    tooltipEl.style.pointerEvents = 'none';
                    tooltipEl.style.position = 'absolute';
                    tooltipEl.style.transform = 'translate(-50%, 0)';
                    tooltipEl.style.transition = 'all .2s ease';
                    chart.canvas.parentNode.appendChild(tooltipEl);
                }

                return tooltipEl;
            };

            return {
                maintainAspectRatio: false,
                aspectRatio: 0.8,
                plugins: {
                    chartAreaBorder: {
                        borderColor: 'red',
                        borderWidth: 2,
                        borderDash: [5, 5],
                        borderDashOffset: 2,
                    },
                    tooltip: {
                        enabled: false,
                        padding: 8,
                        position: 'nearest',
                        external: function (context) {
                            // Tooltip Element
                            const { chart, tooltip } = context;
                            const tooltipEl = getOrCreateTooltip(chart);

                            // Hide if no tooltip
                            if (tooltip.opacity === 0) {
                                tooltipEl.style.opacity = 0;

                                return;
                            }

                            if (tooltip.body) {
                                const bodyLines = tooltip.body.map(b => {
                                    const strArr = b.lines[0].split(':');
                                    const data = {
                                        text: strArr[0].trim(),
                                        value: strArr[1].trim()
                                    }

                                    return data;
                                });

                                // Clear old content
                                tooltipEl.innerHTML = '';
                                bodyLines.forEach((body, i) => {

                                    const text = document.createElement('div');

                                    text.appendChild(document.createTextNode(body.value + '.000'))
                                    text.style.fontWeight = '500'
                                    text.style.lineHeight = '21px'
                                    text.style.fontSize = '14px'
                                    tooltipEl.appendChild(text);
                                });


                            }

                            const { offsetLeft: positionX, offsetTop: positionY } = chart.canvas;

                            // Display, position, and set styles for font
                            tooltipEl.style.opacity = 1;
                            tooltipEl.style.left = positionX + tooltip.caretX + 'px';
                            tooltipEl.style.top = positionY + tooltip.caretY - 40 + 'px';
                            tooltipEl.style.font = tooltip.options.bodyFont.string;
                            tooltipEl.style.padding = tooltip.options.padding + 'px ' + tooltip.options.padding + 'px';
                        }
                    },
                    legend: {
                        display: false,
                    }
                },
                scales: {
                    x: {
                        stacked: true,
                        ticks: {
                            color: textMutedColor,
                            font: {
                                weight: 'lighter'
                            }
                        },
                        grid: {
                            color: 'transparent',
                            borderColor: 'transparent'
                        }
                    },
                    y: {
                        display: false,
                        grace: 14
                    }
                }
            };
        },
    },
    components: {
        Avatar,
        IconField,
        InputIcon,
        InputText,
        Button,
    },
};

</script>
