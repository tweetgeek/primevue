<template>
    <div class="flex-1 h-full overflow-y-auto overflow-x-clip flex border border-surface rounded-xl">
        <div class="flex-[0.25] min-w-40">
            <div class="flex flex-col gap-6 px-5 pt-3">
                <div class="flex items-center justify-between gap-6 text-color">
                    <div class="text-2xl font-medium lead">Chats</div>
                    <Button icon="pi pi-plus" text />
                </div>
                <IconField iconPosition="left">
                    <InputIcon class="pi pi-search"> </InputIcon>
                    <InputText v-model="value1" placeholder="Search" class="w-full" />
                </IconField>
                <SelectButton v-model="value" :options="options" aria-labelledby="basic" />
            </div>
            <div class="flex-1 overflow-y-auto flex flex-col mt-6">
                <div class="flex items-center p-4 cursor-pointer hover:bg-emphasis transition-all">
                    <Avatar label="V" class="mr-2" size="large" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1">
                        <div class="flex items-start gap-1 justify-between">
                            <div class="text-color font-medium leading-6">Cody Fisher</div>
                            <div class="text-sm text-muted-color leading-5">12.30</div>
                        </div>
                        <div class="flex items-center gap-5 justify-between mt-1">
                            <div class="text-muted-color text-sm leading-5 line-clamp-1">Hey there! I've heard about
                                Prim
                            </div>
                            <Badge value="8" severity="contrast"></Badge>
                        </div>
                    </div>
                </div>
                <div class="flex items-center p-4 cursor-pointer hover:bg-emphasis transition-all">
                    <Avatar label="V" class="mr-2" size="large" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1">
                        <div class="flex items-start gap-1 justify-between">
                            <div class="text-color font-medium leading-6">Cody Fisher</div>
                            <div class="text-sm text-muted-color leading-5">12.30</div>
                        </div>
                        <div class="flex items-center gap-5 justify-between mt-1">
                            <div class="text-muted-color text-sm leading-5 line-clamp-1">Hey there! I've heard about
                                Prim
                            </div>
                            <Badge value="8" severity="contrast"></Badge>
                        </div>
                    </div>
                </div>
                <div class="flex items-center p-4 cursor-pointer hover:bg-emphasis transition-all">
                    <Avatar label="V" class="mr-2" size="large" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1">
                        <div class="flex items-start gap-1 justify-between">
                            <div class="text-color font-medium leading-6">Cody Fisher</div>
                            <div class="text-sm text-muted-color leading-5">12.30</div>
                        </div>
                        <div class="flex items-center gap-5 justify-between mt-1">
                            <div class="text-muted-color text-sm leading-5 line-clamp-1">Hey there! I've heard about
                                Prim
                            </div>
                            <Badge value="8" severity="contrast"></Badge>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="flex-[0.5] border-x border-surface flex flex-col">
            <div class="flex items-center p-4 gap-7 border-b border-surface">
                <div class="flex items-center">
                    <Avatar label="V" class="mr-2" size="large" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1">
                        <div class="text-color leading-6">PrimeTek</div>
                        <div class="text-muted-color leading-5 line-clamp-1 mt-1">Cody Fisher, Esther Howard, Jerome
                            Bell,
                            Kristin Watson, Ronald Richards, Darrell Steward</div>
                    </div>
                </div>
                <div class="flex items-center gap-2">
                    <Button icon="pi pi-phone" text />
                    <Button icon="pi pi-search" text />
                    <Button icon="pi pi-ellipsis-h" text />
                </div>
            </div>
            <div class="flex-1 overflow-y-auto flex flex-col gap-8 py-8 px-6">
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full">
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1 bg-surface-100 dark:bg-surface-800 px-2 py-1 rounded-lg">
                        <p class="text-color leading-6 mb-0">Awesome! What's the standout feature?</p>
                    </div>
                </div>
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full">
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1 bg-surface-100 dark:bg-surface-800 px-2 py-1 rounded-lg">
                        <p class="text-color leading-6 mb-0">PrimeVue rocks! Simplifies UI dev with versatile
                            components.</p>
                    </div>
                </div>
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full">
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1 bg-surface-100 dark:bg-surface-800 px-2 py-1 rounded-lg">
                        <p class="text-color leading-6 mb-0">Intriguing! Tell us more about its impact.</p>
                    </div>
                </div>
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full">
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1 bg-surface-100 dark:bg-surface-800 px-2 py-1 rounded-lg">
                        <p class="text-color leading-6 mb-0">It's design-neutral and compatible with Tailwind. Features
                            accessible,
                            high-grade components!</p>
                        <div class="mt-2 w-full h-40 bg-surface-200 dark:bg-surface-700 rounded-lg"></div>
                    </div>
                </div>
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full ml-auto mr-0">
                    <div class="flex-1 bg-primary px-2 py-1 rounded-lg">
                        <p class="text-primary-contrast leading-6 mb-0">Customizable themes, responsive design – UI
                            excellence!</p>
                    </div>
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                </div>
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full">
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1 bg-surface-100 dark:bg-surface-800 px-2 py-1 rounded-lg">
                        <p class="text-color leading-6 mb-0">Love it! Fast-tracking our development is key.</p>
                    </div>
                </div>
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full">
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1 bg-surface-100 dark:bg-surface-800 px-2 py-1 rounded-lg">
                        <p class="text-color leading-6 mb-0">Documentation rocks too – smooth integration for all.</p>
                    </div>
                </div>
                <div class="flex items-start gap-3 min-w-[60%] max-w-[70%] w-full">
                    <Avatar label="V" class="sticky top-0 w-10 h-10" style="background-color: #ece9fc; color: #2a1261"
                        shape="circle" />
                    <div class="flex-1 bg-surface-100 dark:bg-surface-800 px-2 py-1 rounded-lg">
                        <p class="text-color leading-6 mb-0">It's design-neutral and compatible with Tailwind. Features
                            accessible,
                            high-grade components!</p>
                        <div class="mt-2 w-full h-40 bg-surface-200 dark:bg-surface-700 rounded-lg"></div>
                    </div>
                </div>
            </div>
            <div class="p-4 border-t border-surface flex items-center justify-between">
                <div class="flex items-center gap-2 flex-1">
                    <Button icon="pi pi-plus" text />
                    <input class="placeholder:text-muted-color text-color outline-none flex-1 text-base leading-6"
                        style="font-family: inherit;" placeholder="Write your message..." />
                </div>
                <div class="flex items-center gap-2">
                    <Button icon="pi pi-face-smile" text />
                    <Button icon="pi pi-send" />
                </div>
            </div>
        </div>
        <div class="flex-[0.25] min-w-40 py-6 px-3 overflow-auto">
            <div class="flex flex-col items-center justify-center">
                <Avatar label="V" class="w-32 h-32" size="xlarge" style="background-color: #ece9fc; color: #2a1261"
                    shape="circle" />
                <div class="leading-6 font-medium text-color mt-4 w-full text-center">PrimeTek</div>
                <div class="leading-5 text-sm text-muted-color mt-1 w-full text-center">@primetek</div>
                <div class="flex items-center justify-center flex-wrap gap-1 mt-4">
                    <Button icon="pi pi-phone text-muted-color" text />
                    <Button icon="pi pi-video text-muted-color" text />
                    <Button icon="pi pi-sign-in text-muted-color" text />
                    <Button icon="pi pi-info-circle text-muted-color" text />
                    <Button icon="pi pi-ellipsis-v text-muted-color" text />
                </div>
            </div>
            <div class="flex flex-col gap-4 mt-4">
                <div class="flex items-center gap-2">
                    <i class="pi pi-bell text-color"></i>
                    <div class="leading-6 font-medium text-color flex-1">Notification</div>
                    <InputSwitch v-model="notification" />
                </div>
                <div class="flex items-center gap-2">
                    <i class="pi pi-volume-down text-color"></i>
                    <div class="leading-6 font-medium text-color flex-1">Sound</div>
                    <InputSwitch v-model="sound" />
                </div>
                <div class="flex items-center gap-2">
                    <i class="pi pi-download text-color"></i>
                    <div class="leading-6 font-medium text-color flex-1">Save to downloads </div>
                    <InputSwitch v-model="download" />
                </div>
            </div>
            <div class="mt-6">
                <div class="flex items-center gap-2">
                    <div class="flex-1 text-color leading-6 font-medium">Members</div>
                    <Button label="See All" class="text-sm py-0.5 px-2 text-muted-color" text />
                </div>
                <div class="mt-4 flex flex-col gap-4">
                    <div class="flex items-center gap-2 cursor-pointer ">
                        <Avatar label="V" style="background-color: #ece9fc; color: #2a1261" shape="circle" />
                        <div class="text-sm text-color font-medium leading-5 flex-1">Robin Jonas</div>
                        <i class="pi pi-chevron-right text-xs text-muted-color"></i>
                    </div>
                    <div class="flex items-center gap-2 cursor-pointer ">
                        <Avatar label="V" style="background-color: #ece9fc; color: #2a1261" shape="circle" />
                        <div class="text-sm text-color font-medium leading-5 flex-1">Robin Jonas</div>
                        <i class="pi pi-chevron-right text-xs text-muted-color"></i>
                    </div>
                    <div class="flex items-center gap-2 cursor-pointer ">
                        <Avatar label="V" style="background-color: #ece9fc; color: #2a1261" shape="circle" />
                        <div class="text-sm text-color font-medium leading-5 flex-1">Robin Jonas</div>
                        <i class="pi pi-chevron-right text-xs text-muted-color"></i>
                    </div>
                    <div class="flex items-center gap-2 cursor-pointer ">
                        <Avatar label="V" style="background-color: #ece9fc; color: #2a1261" shape="circle" />
                        <div class="text-sm text-color font-medium leading-5 flex-1">Robin Jonas</div>
                        <i class="pi pi-chevron-right text-xs text-muted-color"></i>
                    </div>
                    <div class="flex items-center gap-2 cursor-pointer ">
                        <Avatar label="V" style="background-color: #ece9fc; color: #2a1261" shape="circle" />
                        <div class="text-sm text-color font-medium leading-5 flex-1">Robin Jonas</div>
                        <i class="pi pi-chevron-right text-xs text-muted-color"></i>
                    </div>
                </div>
            </div>
            <div class="mt-5">
                <SelectButton v-model="media" :options="mediaOptions" />
                <div class="mt-3 mb-5 grid grid-cols-3 gap-2">
                    <div
                        class="bg-emphasis hover:opacity-70 transition-all flex-1 aspect-square rounded-lg border border-surface cursor-pointer">

                    </div>
                    <div
                        class="bg-emphasis hover:opacity-70 transition-all flex-1 aspect-square rounded-lg border border-surface cursor-pointer">

                    </div>
                    <div
                        class="bg-emphasis hover:opacity-70 transition-all flex-1 aspect-square rounded-lg border border-surface cursor-pointer">

                    </div>
                    <div
                        class="bg-emphasis hover:opacity-70 transition-all flex-1 aspect-square rounded-lg border border-surface cursor-pointer">

                    </div>
                    <div
                        class="bg-emphasis hover:opacity-70 transition-all flex-1 aspect-square rounded-lg border border-surface cursor-pointer">

                    </div>
                    <div
                        class="bg-emphasis hover:opacity-70 transition-all flex-1 aspect-square rounded-lg border border-surface cursor-pointer">

                    </div>
                </div>
                <Button label="Show more" icon="pi pi-arrow-right" iconPos="right" outlined class="w-full text-left" />
            </div>
        </div>
    </div>
</template>

<script>
import Avatar from '@/components/lib/avatar/Avatar.vue';
import IconField from '@/components/lib/iconfield/IconField.vue'
import InputIcon from '@/components/lib/inputicon/InputIcon.vue'
import InputText from '@/components/lib/inputtext/InputText.vue'
import Button from '@/components/lib/button/Button.vue'
import SelectButton from '@/components/lib/selectbutton/SelectButton.vue'
import Badge from '@/components/lib/badge/Badge.vue'
import InputSwitch from '@/components/lib/inputswitch/InputSwitch.vue'

export default {
    name: 'Overview',
    redrawListener: null,
    data() {
        return {
            download: false,
            notification: true,
            sound: false,
            value: 'Chat',
            value2: '',
            options: ['Chat', 'Call'],
            media: 'Media',
            mediaOptions: ['Media', 'Link', 'Docs'],
            items: Array(5).fill(null)
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
        SelectButton,
        Badge,
        InputSwitch
    },
};

</script>
