<template>
    <div class="inline-block">
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="triforceRequired()">
                <img v-if="countTriforce() > 2" title="TRIFORCE" src="/img/skyward_sword/Full_Triforce_Grid.png" />
                <img v-else-if="countTriforce() > 1" title="2 Triforce" src="/img/skyward_sword/2_Triforce_Grid.png" />
                <img v-else-if="countTriforce()" title="1 Triforce" src="/img/skyward_sword/1_Triforce_Grid.png" />
                <img v-else title="0 Triforce" src="/img/skyward_sword/No_Triforce_Grid.png" />

            </span>

            <img v-if="getNumberItemsFromName('Progressive Sword') > 5" title="True Master Sword" src="/img/skyward_sword/True Master Sword.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Sword') > 4" title="Master Sword" src="/img/skyward_sword/Master Sword.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Sword') > 3" title="Goddess White Sword" src="/img/skyward_sword/Goddess White Sword.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Sword') > 2" title="Goddess Long Sword" src="/img/skyward_sword/Goddess Long Sword.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Sword') > 1" title="Goddess Sword" src="/img/skyward_sword/Goddess Sword.png" />
            <img v-else title="Practice Sword" src="/img/skyward_sword/Practice Sword.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Sword')  }" />
            <span class="mr-2"></span>
            <img src="/img/skyward_sword/emerald_tablet.png" title="Emerald Tablet" :class="{ 'opacity-25': !getNumberItemsFromName('Emerald Tablet')  }" />
            <img src="/img/skyward_sword/ruby_tablet.png" title="Ruby Tablet" :class="{ 'opacity-25': !getNumberItemsFromName('Ruby Tablet')  }" />
            <img src="/img/skyward_sword/amber_tablet.png" title="WhAmbet Tablet" :class="{ 'opacity-25': !getNumberItemsFromName('Amber Tablet')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Inventory</div>

            <img v-if="getNumberItemsFromName('Progressive Mitts') > 1" src="/img/skyward_sword/Mogma_Mitts.png" title="Mogma Mitts" />
            <img v-else src="/img/skyward_sword/Digging_Mitts.png" title="Diggin Mitts" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Mitts')  }" />
            <img src="/img/skyward_sword/Water_Dragon_Scale.png" title="Water Dragon Scale" :class="{ 'opacity-25': !getNumberItemsFromName('Water Dragon\'s Scale')  }" />
            <img title="Scrapper" src="/img/skyward_sword/Scrapper.png" :class="{ 'opacity-25': !getNumberItemsFromName('Scrapper') }" />

            <span class="mr-2"></span>


            <img title="Goddess Harp" :class="{ 'opacity-25': !getNumberItemsFromName('Goddess\'s Harp')  }" src="/img/skyward_sword/Goddess_Harp.png" />

            <img title="Bomb Bag" src="/img/skyward_sword/Bomb_Icon.png" :class="{ 'opacity-25': !bombBag()  }" />
            <img v-if="getNumberItemsFromName('Progressive Beetle') > 1" title="Tough Beetle" src="/img/skyward_sword/Tough_Beetle.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Beetle') > 1" title="Quick Beetle" src="/img/skyward_sword/Quick_Beetle.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Beetle') > 1" title="Hook Beetle" src="/img/skyward_sword/Hook_Beetle.png" />
            <img v-else title="Beetle" src="/img/skyward_sword/Beetle.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Beetle')  }" />
            <img v-if="getNumberItemsFromName('Progressive Bow') > 2" title="Sacred Bow" src="/img/skyward_sword/Sacred_Bow.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Bow') > 1" title="Iron Bow" src="/img/skyward_sword/Iron_Bow.png" />
            <img v-else title="Bow" src="/img/skyward_sword/Bow.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Bow')  }" />
            <img src="/img/skyward_sword/Whip.png" title="Whip" :class="{ 'opacity-25': !getNumberItemsFromName('Whip')  }" />
            <img src="/img/skyward_sword/Clawshots.png" title="Clawshots" :class="{ 'opacity-25': !getNumberItemsFromName('Clawshots')  }" />
            <img v-if="getNumberItemsFromName('Progressive Bug Net') > 1" src="/img/skyward_sword/Big_Bugnet.png" title="Big Bug Net" />
            <img v-else src="/img/skyward_sword/Bugnet.png" title="Bug Net" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Bug Net')  }" />
            <img v-if="getNumberItemsFromName('Progressive Slingshot') > 1" src="/img/skyward_sword/Scattershot.png" title="Scattershot" />
            <img v-else src="/img/skyward_sword/Slingshot.png" title="Slingshot" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Slingshot')  }" />
            <img title="Bottle" src="/img/skyward_sword/bottle.png" :class="{ 'opacity-25': !getNumberItemsFromName('Empty Bottle')  }" />
        </div>
    </div>
</template>
<script>
    /**
    * Skyward Sword
    *
    * Goal is to beat Demise.
    * In order to beat him, you need :
    * - A Master Sword (sword level 3 or 4)
    * - Completed Triforce (if needed)
    *
    */
    export default {
        name: "gDataSkywardSword.vue",
        props: {
            data: Object,
            gamedata: Object,
            index: Number,
            checks_done: Number,
            total_checks: Number,
            player_name: String,
            player_game: String
        },
        data: function () {
            return {
            };
        },
        methods: {
            getGoalDetails: function () {
                if (!this.data.slot_data.hasOwnProperty('got_sword_requirement'))
                    return [];
                var res = [];
                var row_goal = { title: 'Sword Level for Gate of Time', value: '', details: null };
                if (this.data.slot_data.got_sword_requirement == 1)
                    row_goal.value = '1 (Training Sword)';
                else if (this.data.slot_data.got_sword_requirement == 2)
                    row_goal.value = '2 (Goddess Sword)';
                else if (this.data.slot_data.got_sword_requirement == 3)
                    row_goal.value = '3 (Long Goddess Sword)';
                else if (this.data.slot_data.got_sword_requirement == 4)
                    row_goal.value = '4 (White Goddess Sword)';
                else if (this.data.slot_data.got_sword_requirement == 5)
                    row_goal.value = '5 (Master Sword)';
                else if (this.data.slot_data.got_sword_requirement == 6)
                    row_goal.value = '6 (True Master Sword)';

                res.push(row_goal);

                row_goal = { title: 'Dungeons for Gate of Time', value: this.data.slot_data.got_dungeon_requirement, details: null };

                res.push(row_goal);



                return res;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            triforceRequired: function () {
                if (this.data.slot_data.hasOwnProperty('triforce_required'))
                    return this.data.slot_data.triforce_required;
                return true;
            },
            countTriforce: function () {
                return this.$parent.getNumberItemsFromGroup(['Triforce of Courage', 'Triforce of Wisdom', 'Triforce of Power']);
            },
            bombBag: function () {
                if (this.$parent.getNumberItemsFromGroup(['Bomb Bag', 'Small Bomb Bag'])) {
                    return true;
                }
                return false;
            }
        },
        components: {
        },
    };
</script>
