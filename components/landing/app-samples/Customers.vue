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
                            <Button icon="pi pi-ellipsis-h" outlined severity="secondary" />
                        </div>
                    </template>
                </Column>
            </DataTable>
        </div>
    </div>
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
