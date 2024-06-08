<template>
    <div class="flex-1 h-full overflow-y-auto overflow-x-clip overflow-hidden border border-surface rounded-xl p-6">
        <div class="text-color text-2xl font-medium leading-8">Cards</div>
        <div class="mt-1 text-muted-color leading-6">You can make cards using Aura like below 👇</div>
        <div class="mt-6 flex items-start gap-6">
            <div class="flex-1 flex flex-col gap-6">
                <div class="border border-surface rounded-3xl p-6 flex flex-col gap-6">
                    <div class="flex items-center gap-3">
                        <OverlayBadge severity="danger" class="w-fit">
                            <Avatar image="/demo/images/main-avatar.png" size="large"
                                class="rounded-lg overflow-hidden" />
                        </OverlayBadge>
                        <div>
                            <div class="font-medium text-color leading-6">Jacob Jones</div>
                            <div class="mt-1 text-muted-color leading-5">hi@jacobjones.co</div>
                        </div>
                    </div>
                    <div class="flex items-center gap-6">
                        <div class="text-sm leading-5 text-color">
                            14.k <span class="text-muted-color">Followers</span>
                        </div>
                        <div class="text-sm leading-5 text-color">
                            359 <span class="text-muted-color">Following</span>
                        </div>
                    </div>
                    <p class="text-sm text-muted-color leading-5 mb-0">
                        Meet Jacob Jones, the whimsical adventurer on a quest for life's quirks. From sock mysteries to
                        subway adventures, join him for a laughter-filled journey!
                    </p>
                    <div class="flex items-center justify-between gap-2">
                        <div class="text-sm leading-5 text-color font-medium">Mutual Friends</div>
                        <AvatarGroup>
                            <Avatar image="/demo/images/avatar1.png" size="small" class="rounded-lg overflow-hidden" />
                            <Avatar image="/demo/images/avatar2.png" size="small" class="rounded-lg overflow-hidden" />
                            <Avatar image="/demo/images/avatar3.png" size="small" class="rounded-lg overflow-hidden" />
                            <Avatar image="/demo/images/avatar4.png" size="small" class="rounded-lg overflow-hidden" />
                            <Avatar image="/demo/images/avatar5.png" size="small" class="rounded-lg overflow-hidden" />
                            <Avatar label="+99" size="small" class="rounded-lg overflow-hidden text-xs" />
                        </AvatarGroup>
                    </div>
                    <SelectButton v-model="selectedUserSelectButtonOption" :options="userSelectButtonOptions" :pt="{
                        root: {
                            class: 'flex items-center [&>*]:flex-1'
                        },
                    }" />
                    <div class="flex flex-col gap-4">
                        <div class="p-2 rounded-2xl flex items-center gap-3 bg-emphasis">
                            <OverlayBadge severity="danger" class="w-fit">
                                <Avatar image="/demo/images/main-avatar.png"
                                    class="rounded-lg overflow-hidden w-10 h-10" />
                            </OverlayBadge>
                            <div class="flex-1">
                                <div class="text-color text-sm font-medium leading-5">Jacob Jones</div>
                                <div class="mt-1 text-muted-color text-xs leading-4">hi@jacobjones.co</div>
                            </div>
                            <Button label="Join" />
                        </div>
                        <div class="p-2 rounded-2xl flex items-center gap-3 bg-emphasis">
                            <OverlayBadge severity="danger" class="w-fit">
                                <Avatar image="/demo/images/avatar4.png" class="rounded-lg overflow-hidden w-10 h-10" />
                            </OverlayBadge>
                            <div class="flex-1">
                                <div class="text-color text-sm font-medium leading-5">Courtney Henry</div>
                                <div class="mt-1 text-muted-color text-xs leading-4">cou.henry41@courtney.co</div>
                            </div>
                            <Button label="Join" />
                        </div>
                    </div>
                </div>
                <div class="border border-surface rounded-3xl p-6">
                    <div
                        class="flex items-center gap-3 p-3 border border-surface rounded-xl shadow-[0px_1px_2px_0px_rgba(18,18,23,0.05)]">
                        <Avatar image="/demo/images/main-avatar.png" class="rounded-lg overflow-hidden w-14 h-14" />
                        <div class="flex-1">
                            <div class="text-color font-medium leading-7">Jacob Jones</div>
                            <div class="text-muted-color text-sm mt-1">hi@jacobjones.co</div>
                        </div>
                        <Button icon="pi pi-bell" severity="contrast" text />
                    </div>
                    <div class="mt-4 flex flex-col gap-2">
                        <button
                            class="w-full flex items-center gap-2 text-color p-2 bg-transparent hover:bg-emphasis active:bg-surface-200 dark:active:bg-surface-700 cursor-pointer rounded-lg transition-all select-none">
                            <i class="pi pi-envelope text-lg w-7 h-7 flex items-center justify-center"></i>
                            <div class="font-medium leading-normal flex-1 text-left">Messages</div>
                        </button>
                        <button
                            class="w-full flex items-center gap-2 text-color p-2 bg-transparent hover:bg-emphasis active:bg-surface-200 dark:active:bg-surface-700 cursor-pointer rounded-lg transition-all select-none">
                            <i class="pi pi-cog text-lg w-7 h-7 flex items-center justify-center"></i>
                            <div class="font-medium leading-normal flex-1 text-left">Settings</div>
                        </button>
                        <button
                            class="w-full flex items-center gap-2 text-color p-2 bg-transparent hover:bg-emphasis active:bg-surface-200 dark:active:bg-surface-700 cursor-pointer rounded-lg transition-all select-none">
                            <i class="pi pi-sync text-lg w-7 h-7 flex items-center justify-center"></i>
                            <div class="font-medium leading-normal flex-1 text-left">Switch Accounts</div>
                        </button>
                        <button
                            class="w-full flex items-center gap-2 text-color p-2 bg-transparent hover:bg-emphasis active:bg-surface-200 dark:active:bg-surface-700 cursor-pointer rounded-lg transition-all select-none">
                            <i class="pi pi-sign-in text-lg w-7 h-7 flex items-center justify-center"></i>
                            <div class="font-medium leading-normal flex-1 text-left">Log out</div>
                        </button>
                    </div>
                    <Divider />
                    <button @click="darkMode = !darkMode"
                        class="w-full flex items-center gap-2 text-color p-2 bg-transparent hover:bg-emphasis active:bg-surface-200 dark:active:bg-surface-700 cursor-pointer rounded-lg transition-all select-none">
                        <i class="pi text-lg w-7 h-7 flex items-center justify-center" :class="{
                            'pi-moon': !darkMode,
                            'pi-sun': darkMode
                        }"></i>
                        <div class="font-medium leading-normal flex-1 text-left">Switch to {{ darkMode ? 'Light' :
                            'Dark' }}
                        </div>
                        <InputSwitch v-model="darkMode" class="pointer-events-none" />
                    </button>
                </div>
                <div class="border border-surface rounded-3xl">
                    <div class="p-6 flex flex-col gap-6">
                        <div class="flex items-start gap-2 justify-between">
                            <div>
                                <div class="text-2xl text-color font-medium">Data Analyst </div>
                                <div class="mt-2 text-color">Data Insights Ltd.</div>
                            </div>
                            <Button icon="pi pi-bookmark" severity="secondary" outlined rounded />
                        </div>
                        <div class="flex flex-wrap gap-1 items-center justify-between">
                            <div class="flex items-center gap-2 whitespace-nowrap text-muted-color">
                                <i class="pi pi-users text-xl"></i>
                                <div class="font-medium leading-none">Senior</div>
                            </div>
                            <div class="flex items-center gap-2 whitespace-nowrap text-muted-color">
                                <i class="pi pi-stopwatch text-xl"></i>
                                <div class="font-medium leading-none">Full-Time</div>
                            </div>
                            <div class="flex items-center gap-2 whitespace-nowrap text-muted-color">
                                <i class="pi pi-money-bill text-xl"></i>
                                <div class="font-medium leading-none">$80,000</div>
                            </div>
                        </div>
                        <p class="leading-6 text-muted-color mb-0">
                            Expert in data analysis? Join Data Insights Ltd. as a senior data analyst. Lead in the world
                            of data with us!
                        </p>
                        <div class="flex flex-wrap gap-2 items-center">
                            <Tag value="Data Analysis" rounded class="font-normal"></Tag>
                            <Tag value="Analytics" rounded class="font-normal"></Tag>
                            <Tag value="Big Data" rounded class="font-normal"></Tag>
                        </div>
                    </div>
                </div>
            </div>
            <div class="flex-1 flex flex-col gap-6">
                <div class="border border-surface rounded-3xl p-6">

                </div>
            </div>
            <div class="flex-1 flex flex-col gap-6">
                <div class="border border-surface rounded-3xl p-6">
                    <div class="text-color font-medium leading-6 mb-4">User Profiles</div>
                    <SelectButton v-model="userProfiles" :options="userProfilesOptions" :pt="{
                        root: {
                            class: 'flex items-center [&>*]:flex-1'
                        },
                    }" />
                    <div class="flex flex-col gap-4 mt-6">
                        <div class="flex items-center gap-3">
                            <i class="pi pi-volume-down text-color text-xl"></i>
                            <div class="leading-6 text-color flex-1">Sound</div>
                            <InputSwitch v-model="userProfilesValues[0]" />
                        </div>
                        <div class="flex items-center gap-3">
                            <i class="pi pi-wifi text-color text-xl"></i>
                            <div class="leading-6 text-color flex-1">Wi-Fi</div>
                            <InputSwitch v-model="userProfilesValues[1]" />
                        </div>
                        <div class="flex items-center gap-3">
                            <i class="pi pi-moon text-color text-xl"></i>
                            <div class="leading-6 text-color flex-1">Dark Mode</div>
                            <InputSwitch v-model="userProfilesValues[2]" />
                        </div>
                        <div class="flex items-center gap-3">
                            <i class="pi pi-map-marker text-color text-xl"></i>
                            <div class="leading-6 text-color flex-1">Location Services</div>
                            <InputSwitch v-model="userProfilesValues[3]" />
                        </div>
                        <div class="flex items-center gap-3">
                            <i class="pi pi-shield text-color text-xl"></i>
                            <div class="leading-6 text-color flex-1">Privacy Settings</div>
                            <InputSwitch v-model="userProfilesValues[4]" />
                        </div>
                        <div class="flex items-center gap-3">
                            <i class="pi pi-sync text-color text-xl"></i>
                            <div class="leading-6 text-color flex-1">Auto Update</div>
                            <InputSwitch v-model="userProfilesValues[5]" />
                        </div>
                    </div>
                </div>
                <div class="border border-surface rounded-3xl p-6 flex flex-col gap-6">
                    <div class="font-medium text-color text-2xl text-center">Forgot Password</div>
                    <div>
                        <div class="text-muted-color text-lg text-center leading-snug">Verification code <br />
                            has been sent to email</div>
                        <div
                            class="rounded-full px-4 py-1 bg-surface-200 dark:bg-surface-800 w-fit mx-auto mt-4 text-color text-lg leading-relaxed">
                            u*******m@gmail.com</div>
                    </div>
                    <div class="flex items-center justify-center">
                        <Button label="Resend" text />
                    </div>
                    <div class="flex items-center justify-center">
                        <InputOtp v-model="forgotPasswordOTP" :length="6" />
                    </div>
                    <Button label="Change password" />
                </div>
                <div class="border border-surface rounded-3xl p-6">
                    <div class="text-color font-medium leading-6 mb-6">Price Range</div>
                    <div>
                        <Slider v-model="priceRange" :min="0" range :max="15000" />
                    </div>
                    <div class="mt-4 flex gap-2">
                        <div class="flex-1">
                            <label for="price-min-val" class="leading-6 text-color">Min Value</label>
                            <InputNumber v-model="priceRange[0]" :min="0" inputId="price-min-val" mode="currency"
                                currency="USD" locale="en-US" :pt="{
                                    root: {
                                        class: '[&>*]:w-full mt-2'
                                    }
                                }" />
                        </div>
                        <div class="flex-1">
                            <label for="price-max-val" class="leading-6 text-color">Max Value</label>
                            <InputNumber v-model="priceRange[1]" inputId="price-max-val" mode="currency" currency="USD"
                                locale="en-US" :pt="{
                                    root: {
                                        class: '[&>*]:w-full mt-2'
                                    }
                                }" />
                        </div>
                    </div>
                    <div class="mt-4">
                        <div class="text-color font-medium leading-6 mb-6">Popular specs</div>
                        <div class="flex items-center gap-4 flex-wrap">
                            <div v-for="(data, index) of priceRangePopularSpecs" :key="index"
                                class="flex align-items-center">
                                <Checkbox v-model="priceRangePopularSpecsChecked[index]" :inputId="data.value"
                                    name="price" :value="data.value" />
                                <label :for="data.value" class="ml-2">{{ data.value }}</label>
                            </div>
                        </div>
                    </div>
                    <div class="flex items-center gap-3 flex-wrap [&>*]:flex-1 mt-6">
                        <Button label="Undo" outlined />
                        <Button label="Random" />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Avatar from '@/components/lib/avatar/Avatar.vue';
import Button from '@/components/lib/button/Button.vue';
import InputSwitch from '@/components/lib/inputswitch/InputSwitch.vue';
import SelectButton from '@/components/lib/selectbutton/SelectButton.vue';

export default {
    name: 'Cards',
    redrawListener: null,
    data() {
        return {
            userProfiles: 'Chilling',
            userProfilesOptions: ['Chilling', 'Do Not Disturb'],
            userProfilesValues: [true, true, false, false, true, false],
            forgotPasswordOTP: '023',
            priceRange: [0, 10000],
            priceMinVal: 0,
            priceMaxVal: 100000,
            priceRangePopularSpecs: [
                { value: 'Furnished', checked: true },
                { value: 'Unfurnished', checked: false },
                { value: 'Detached', checked: true },
                { value: 'Underfloor heating', checked: false },
                { value: 'Balcony', checked: true },
                { value: 'Duplex', checked: false },
                { value: 'Triplex', checked: false },
                { value: 'Garden', checked: false },
                { value: 'Central location', checked: false },
                { value: 'Sea view', checked: true },
            ],
            priceRangePopularSpecsChecked: [true, false, true, false, true, false, false, false, false, true],
            userSelectButtonOptions: ['Joined', 'Hosted'],
            selectedUserSelectButtonOption: 'Joined',
            darkMode: false,
        };
    },
    methods: {
    },
    components: {
        Avatar,
        Button,
        SelectButton,
        InputSwitch
    },
};

</script>
