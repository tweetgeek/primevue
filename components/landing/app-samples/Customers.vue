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
        <div class="flex-1 rounded-lg border border-surface w-full overflow-auto">
            <DataTable v-model:selection="selectedRows" selectionMode="multiple" :value="tableData"
                class="[&>td]:border-0" :rows="10" :pt="{
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
                            <Avatar v-bind="data.image ? { image: data.image } : { label: data.capName }" :class="{
                                'bg-violet-100 text-violet-950 text-xs font-medium': !data.image
                            }" class="mr-4 rounded-md overflow-hidden" />
                            <div class="leading-6 text-color font-medium">{{ data.name }}</div>
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
                            <svg xmlns="http://www.w3.org/2000/svg" width="19" height="19" viewBox="0 0 19 19"
                                fill="none">
                                <g clip-path="url(#clip0_536_12476)">
                                    <path fill-rule="evenodd" clip-rule="evenodd"
                                        d="M6.82207 0.728516C5.83146 0.728516 4.88145 1.12203 4.18099 1.82249L1.89501 4.10846C1.19454 4.80892 0.801025 5.75895 0.801025 6.74956C0.801025 7.8426 1.27054 8.82597 2.01888 9.509C1.27054 10.192 0.801025 11.1754 0.801025 12.2684C0.801025 13.2591 1.19454 14.2091 1.89501 14.9095L4.18099 17.1955C4.88145 17.896 5.83146 18.2895 6.82207 18.2895C7.91511 18.2895 8.89848 17.82 9.58152 17.0716C10.2646 17.82 11.2479 18.2895 12.341 18.2895C13.3316 18.2895 14.2816 17.896 14.982 17.1955L17.268 14.9095C17.9685 14.2091 18.362 13.2591 18.362 12.2684C18.362 11.1754 17.8925 10.192 17.1442 9.509C17.8925 8.82597 18.362 7.8426 18.362 6.74956C18.362 5.75895 17.9685 4.80892 17.268 4.10846L14.982 1.82249C14.2816 1.12203 13.3316 0.728516 12.341 0.728516C11.2479 0.728516 10.2646 1.19802 9.58152 1.94637C8.89848 1.19802 7.91511 0.728516 6.82207 0.728516ZM11.9859 9.62736C12.0509 9.56231 12.0509 9.45569 11.9859 9.39064L11.4907 8.89547C10.4363 7.84105 8.72674 7.84105 7.67233 8.89547L7.17716 9.39064C7.11211 9.45569 7.11211 9.56231 7.17716 9.62736L7.67233 10.1225C8.72674 11.177 10.4363 11.177 11.4907 10.1225L11.9859 9.62736ZM11.0796 13.2931C10.7451 13.6276 10.5571 14.0814 10.5571 14.5544C10.5571 15.5396 11.3558 16.3383 12.341 16.3383C12.8141 16.3383 13.2678 16.1503 13.6023 15.8158L15.8883 13.5298C16.2229 13.1953 16.4108 12.7415 16.4108 12.2684C16.4108 11.2833 15.6121 10.4846 14.627 10.4846C14.1539 10.4846 13.7001 10.6725 13.3656 11.0071L11.0796 13.2931ZM8.60592 14.5544C8.60592 14.0814 8.41798 13.6276 8.08345 13.2931L5.79743 11.0071C5.4629 10.6725 5.00918 10.4846 4.53608 10.4846C3.5509 10.4846 2.75224 11.2833 2.75224 12.2684C2.75224 12.7415 2.94018 13.1953 3.27471 13.5298L5.56071 15.8158C5.89525 16.1503 6.34898 16.3383 6.82207 16.3383C7.80724 16.3383 8.60592 15.5396 8.60592 14.5544ZM8.60592 4.46357C8.60592 4.93666 8.41798 5.39037 8.08346 5.72489L5.79743 8.01092C5.4629 8.34545 5.00918 8.5334 4.53608 8.5334C3.5509 8.5334 2.75224 7.73473 2.75224 6.74956C2.75224 6.27646 2.94018 5.82274 3.27471 5.48821L5.56071 3.20221C5.89525 2.86767 6.34898 2.67974 6.82207 2.67974C7.80724 2.67974 8.60592 3.47838 8.60592 4.46357ZM13.3656 8.01092L11.0796 5.72489C10.7451 5.39037 10.5571 4.93666 10.5571 4.46357C10.5571 3.47838 11.3558 2.67974 12.341 2.67974C12.8141 2.67974 13.2678 2.86767 13.6023 3.20221L15.8883 5.48821C16.2229 5.82274 16.4108 6.27646 16.4108 6.74956C16.4108 7.73473 15.6121 8.5334 14.627 8.5334C14.1539 8.5334 13.7001 8.34545 13.3656 8.01092Z"
                                        fill="#52525A" />
                                </g>
                                <defs>
                                    <clipPath id="clip0_536_12476">
                                        <rect width="17.561" height="18" fill="white"
                                            transform="translate(0.800049 0.5)" />
                                    </clipPath>
                                </defs>
                            </svg>
                            <div class="leading-6 text-surface-600 dark:text-surface-400">{{ data.company }}</div>
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
                class: '!max-w-[35.5rem] !w-full !h-[100vh] rounded-l-2xl'
            },
            footer: {
                class: 'hidden'
            },
            content: {
                class: 'flex-1 flex flex-col'
            }
        }">
        <template #container="{ closeCallback }">
            <div class="flex flex-col h-[100vh] overflow-auto">
                <div class="">
                    <div class="flex align-items-center gap-3 p-6">
                        <Avatar image="/demo/images/avatar1.png" size="large" class="rounded-xl overflow-hidden" />
                        <div class="flex-1">
                            <div class="leading-6 text-color font-medium">Brook Simmons</div>
                            <div class="mt-1 leading-5 text-muted-color text-sm">Sales Executive </div>
                        </div>
                        <Button icon="pi pi-sign-out" text rounded severity="secondary" />
                    </div>
                    <SelectButton v-model="selectedSidebarOption" :options="sidebarOptions" :pt="{
                        root: {
                            class: 'px-6 py-3 flex items-center [&>*]:flex-1 ![&>*]:text-sm'
                        },
                        button: {
                            class: '!text-sm'
                        }
                    }" />
                </div>
                <div v-if="selectedSidebarOption === 'Interaction Logs'"
                    class="h-[calc(100%-160px)] flex flex-col gap-4 p-6">
                    <div class="h-1/3 flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="flex items-start justify-between">
                            <div class="leading-6 font-medium text-color">Call Logs</div>
                            <Button icon="pi pi-download text-sm" class="w-8 h-8" severity="contrast" />
                        </div>
                        <div
                            class="overflow-y-auto flex-1 bg-surface-0 dark:bg-surface-900 mt-2 flex flex-col rounded-lg overflow-hidden divide-y divide-surface-200 dark:divide-surface-800">
                            <div class="flex items-center gap-3 p-2">
                                <Avatar image="/demo/images/avatar1.png" size="small"
                                    class="rounded-md overflow-hidden w-10 h-10" />
                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color">Brook Simmons</div>
                                    <div class="mt-1 text-sm leading-5 text-muted-color">02.02.2024 | 45 min</div>
                                </div>
                                <Button icon="pi pi-phone" />
                            </div>
                            <div class="flex items-center gap-3 p-2">
                                <Avatar image="/demo/images/avatar1.png" size="small"
                                    class="rounded-md overflow-hidden w-10 h-10" />
                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color">Brook Simmons</div>
                                    <div class="mt-1 text-sm leading-5 text-muted-color">02.02.2024 | 45 min</div>
                                </div>
                                <Button icon="pi pi-phone" />
                            </div>
                            <div class="flex items-center gap-3 p-2">
                                <Avatar image="/demo/images/avatar1.png" size="small"
                                    class="rounded-md overflow-hidden w-10 h-10" />
                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color">Brook Simmons</div>
                                    <div class="mt-1 text-sm leading-5 text-muted-color">02.02.2024 | 45 min</div>
                                </div>
                                <Button icon="pi pi-phone" />
                            </div>
                        </div>
                    </div>
                    <div class="h-1/3 flex flex-col flex-1 p-3 rounded-xl bg-emphasis">
                        <div class="flex items-start justify-between">
                            <div class="leading-6 font-medium text-color">Email Records</div>
                            <Button icon="pi pi-download text-sm" class="w-8 h-8" severity="contrast" />
                        </div>
                        <div
                            class="overflow-y-auto flex-1 bg-surface-0 dark:bg-surface-900 mt-2 flex flex-col rounded-lg overflow-hidden divide-y divide-surface-200 dark:divide-surface-800">
                            <div class="flex items-center gap-3 p-2">
                                <Avatar image="/demo/images/avatar5.png" size="small"
                                    class="rounded-md overflow-hidden w-10 h-10" />
                                <div class="flex-[0.45] text-sm leading-5 font-medium text-color">Jane Cooper</div>
                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color line-clamp-2 max-w-56">
                                        Unleash Business Potential
                                        <span class="text-muted-color ">
                                            Automate, analyze, and accelerate with our SaaS platform. Unshackle from
                                            mundane
                                        </span>
                                    </div>
                                    <div class="mt-1  "> </div>
                                </div>
                                <div class="text-sm leading-5 text-muted-color">3:24 PM </div>
                            </div>
                            <div class="flex items-center gap-3 p-2">
                                <Avatar image="/demo/images/avatar1.png" size="small"
                                    class="rounded-md overflow-hidden w-10 h-10" />
                                <div class="flex-[0.45] text-sm leading-5 font-medium text-color">Cody Fisher</div>
                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color line-clamp-2 max-w-56">
                                        Optimized Workflow Revolution
                                        <span class="text-muted-color ">
                                            Experience a workflow revolution with our intuitive SaaS tool. With enhanced
                                        </span>
                                    </div>
                                    <div class="mt-1  "> </div>
                                </div>
                                <div class="text-sm leading-5 text-muted-color">12.23.2023</div>
                            </div>
                            <div class="flex items-center gap-3 p-2">
                                <Avatar image="/demo/images/avatar4.png" size="small"
                                    class="rounded-md overflow-hidden w-10 h-10" />
                                <div class="flex-[0.45] text-sm leading-5 font-medium text-color">Darrell Steward</div>
                                <div class="flex-1">
                                    <div class="text-sm leading-5 font-medium text-color line-clamp-2 max-w-56">
                                        Innovation at Fingertips
                                        <span class="text-muted-color ">
                                            With our SaaS solution, innovation is only a click away
                                        </span>
                                    </div>
                                    <div class="mt-1  "> </div>
                                </div>
                                <div class="text-sm leading-5 text-muted-color">12.17.2023</div>
                            </div>
                        </div>
                    </div>
                    <div class="h-1/3 flex flex-col flex-1 p-3 rounded-xl bg-emphasis">
                        <div class="flex items-start justify-between">
                            <div class="leading-6 font-medium text-color">Meeting Notes</div>
                            <Button icon="pi pi-download text-sm" class="w-8 h-8" severity="contrast" />
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
                <div v-if="selectedSidebarOption === 'Preferences'"
                    class="h-[calc(100%-160px)] flex flex-col gap-4 p-6">
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
                <div v-if="selectedSidebarOption === 'Opportunities'"
                    class="h-[calc(100%-160px)] grid grid-cols-2 gap-6 p-6">
                    <div v-for="(data, i) of opportunities" :key="i" class="flex flex-col p-3 rounded-xl bg-emphasis">
                        <div class="flex items-center justify-between gap-2">
                            <div class="font-medium text-color">{{ data.title }}</div>
                            <Button icon="pi pi-arrow-up-right" />
                        </div>
                        <img class="flex-1 w-full rounded-lg mt-2 block" :src="data.image" alt="Opportunutiy Image" />
                        <div class="flex-1 mt-2 p-2 rounded-lg bg-surface-0 dark:bg-surface-900 text-xs text-color">
                            {{ data.text }}
                        </div>
                    </div>
                </div>
                <div v-if="selectedSidebarOption === 'Statistics'" class="h-[calc(100%-160px)] p-6">
                    <div class="grid grid-cols-2 gap-4 h-2/3">
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="flex items-center justify-between gap-2">
                                <div class="font-medium text-color p-2">Customer Satisfaction Score</div>
                            </div>
                            <div
                                class="flex-1 mt-2 flex items-center justify-center rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                                <Knob v-model="customerSatisfaction" :size="120" valueTemplate="{value}%" />
                            </div>
                        </div>
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="flex items-center justify-between gap-2">
                                <div class="font-medium text-color p-2">Estimated Lifetime Value</div>
                            </div>
                            <div class="flex-1 mt-2 p-2 rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                            </div>
                        </div>
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="flex items-center justify-between gap-2">
                                <div class="font-medium text-color p-2">Product Usage</div>
                            </div>
                            <div class="flex-1 mt-2 p-2 rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                            </div>
                        </div>
                        <div class="w-full h-full flex flex-col p-3 rounded-xl bg-emphasis">
                            <div class="font-medium text-color p-2">Churn Risk</div>
                            <div
                                class="flex-1 mt-2 flex items-center justify-center rounded-lg bg-surface-0 dark:bg-surface-900 shadow-sm">
                                <Knob v-model="churnRisk" :size="120" valueTemplate="{value}%" />
                            </div>
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
export default {
    name: 'Inbox',
    redrawListener: null,
    data() {
        return {
            tableData: [
                { id: 1, image: '/demo/images/avatar1.png', active: false, name: 'Brook Simmons', title: 'Sales Executive ', company: 'Mistranet', email: 'hi@brooksmmns.co', lead: 'Linkedin', status: 'Active' },
                { id: 2, image: '/demo/images/avatar2.png', active: false, name: 'Dianne Russell', title: 'CEO', company: 'BriteMank', email: 'hi@diannerussell.com', lead: 'Website', status: 'Inactive' },
                { id: 3, image: '/demo/images/avatar3.png', active: false, name: 'Amy Elsner', title: 'Product Manager', company: 'Limerantz', email: 'hi@amyelsner.com', lead: 'Cold Call', status: 'Prospect' },
                { id: 4, image: '/demo/images/avatar4.png', active: false, name: 'Jacob Jones', title: 'Manager', company: 'Streamlinz', email: 'jacobjones@gmail.com', lead: 'Partner', status: 'Prospect' },
                { id: 5, image: '', active: false, name: 'Cameron Watson', capName: 'CW', title: 'Product Manager', company: 'Trimzales', email: 'hi@cameronwilliamson', lead: 'Social Media', status: 'Active' },
                { id: 6, image: '', active: false, name: 'Wade Warren', capName: 'WW', title: 'Director', company: 'ZenTrailMs', email: 'hi@annetteblack.com', lead: 'Cold Call', status: 'Inactive' },
                { id: 7, image: '/demo/images/avatar7.png', active: false, name: 'Guy Hawkins', title: 'Director', company: 'Wavelength', email: 'hi@darrellsteward.com', lead: 'Linkedin', status: 'Active' },
                { id: 8, image: '/demo/images/avatar8.png', active: false, name: 'Annette Black', title: 'Manager', company: 'AlphaHex', email: 'jeromebell@gmail.com', lead: 'Website', status: 'Inactive' },
                { id: 9, image: '/demo/images/avatar1.png', active: false, name: 'Darrell Steward', title: 'Product Manager', company: 'Trimzales', email: 'hi@onyamalimba.co', lead: 'Website', status: 'Active' },
                { id: 10, image: '', active: false, name: 'Jerome Bell', capName: 'JB', title: 'Marketing Manager', company: 'BriteMank', email: 'hi@courtneyhenryo', lead: 'Social Media', status: 'Active' },
                { id: 11, image: '/demo/images/avatar1.png', active: false, name: 'Onyama Limba', title: 'Sales Executive ', company: 'Limerantz', email: 'hi@arlenemccoy.com', lead: 'Social Media', status: 'Active' },
            ],
            selectedRows: [],
            visibleRight: false,
            selectedSidebarOption: 'Interaction Logs',
            sidebarOptions: ['Interaction Logs', 'Preferences', 'Statistics', 'Opportunities'],
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
                { title: 'Apollo', image: 'https://primefaces.org/cdn/primevue/images/layouts/apollo-vue.jpg', text: "Keep your application fresh with Apollo, the newest and most modern template available." },
                { title: 'Ultima', image: 'https://primefaces.org/cdn/primevue/images/layouts/ultima-vue.jpg', text: "Elevate your application's intuitiveness with Ultima's premium Material Design interface." },
                { title: 'Diamond', image: 'https://primefaces.org/cdn/primevue/images/layouts/diamond-vue.jpg', text: "Handle complex operations with elegance with Diamond's robust and powerful premium design." },
                { title: 'Atlantis', image: 'https://primefaces.org/cdn/primevue/images/layouts/atlantis-vue.jpg', text: "Boost your application's capabilities, customization with the Atlantis template." },
                { title: 'Verona', image: 'https://primefaces.org/cdn/primevue/images/layouts/verona-vue.jpg', text: "Achieve sophistication and subtlety with Verona's minimalistic, content-focused design." },
                { title: 'Freya', image: 'https://primefaces.org/cdn/primevue/images/layouts/freya-vue.png', text: "Give your application a sleek, updated look with Freya's chic and modern premium template." },
            ],
            customerSatisfaction: 56,
            churnRisk: 24,
        };
    },
    methods: {

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
