<template>
    <div class="inline-block">
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>
            <span class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Fused Shadow')  }"><img title="Fused Shadow" src="/img/twilight_princess/shadow3.png" />x{{ getNumberItemsFromName('Progressive Fused Shadow') }} </span> / 3</span>

            <img title="Shadow Crystal" :class="{ 'opacity-25': !getNumberItemsFromName('Shadow Crystal')  }" src="/img/twilight_princess/shad_crystal.png" />
            <img v-if="getNumberItemsFromName('Progressive Master Sword') > 3" title="Blessed Master Sword" src="/img/twilight_princess/23_3.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Master Sword') > 2" title="Master Sword" src="/img/twilight_princess/23_1.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Master Sword') > 1" title="Orlin Sword" src="/img/twilight_princess/22_1.png" />
            <img v-else title="Wooden Sword" src="/img/twilight_princess/47_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Master Sword')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Inventory</div>
            <span v-if="closedPalaceOfTwilight()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Mirror Shard')  }"><img title="Mirror Shard" src="/img/twilight_princess/shard4.png" />x{{ getNumberItemsFromName('Progressive Mirror Shard') }} </span> / 4</span>

            <span v-if="closedSkyCity()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Sky Book')  }"><img title="Sky Book" src="/img/twilight_princess/skybook.png" />x{{ getNumberItemsFromName('Progressive Sky Book') }} </span> / 7</span>

            <span v-if="closedSkyCity() || closedPalaceOfTwilight()" class="mr-2"></span>

            <img title="Iron Boots" src="/img/twilight_princess/iron_boots.png" :class="{ 'opacity-25': !getNumberItemsFromName('Iron Boots')  }" />
            <img src="/img/twilight_princess/zora_armor.png" title="Zora Armor" :class="{ 'opacity-25': !getNumberItemsFromName('Zora Armor')  }" />

            <span class="mr-2"></span>


            <img src="/img/twilight_princess/35_1.png" title="Horse Call" :class="{ 'opacity-25': !getNumberItemsFromName('Horse Call')  }" />
            <img title="Bomb Bag" src="/img/twilight_princess/bombbag.png" :class="{ 'opacity-25': !getNumberItemsFromName('Bomb Bag')  }" />
            <img title="Gale Boomerang" src="/img/twilight_princess/boomerang.png" :class="{ 'opacity-25': !getNumberItemsFromName('Gale Boomerang')  }" />
            <img v-if="getNumberItemsFromName('Progressive Hero\'s Bow')" src="/img/twilight_princess/bow.png" title="Bow" />
            <img v-else src="/img/twilight_princess/slingshot.png" title="Slingshot" :class="{ 'opacity-25': !getNumberItemsFromName('Slingshot')  }" />

            <img v-if="getNumberItemsFromName('Progressive Clawshot') > 1" title="Double Clawshot" src="/img/twilight_princess/clawshot2.png" />
            <img v-else src="/img/twilight_princess/clawshot.png" title="Clawshot" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Clawshot')  }" />
            <img title="Ball and Chain" src="/img/twilight_princess/chainball.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ball and Chain')  }" />
            <img title="Drehen" src="/img/twilight_princess/spinner.png" :class="{ 'opacity-25': !getNumberItemsFromName('Spinner')  }" />
            <img v-if="getNumberItemsFromName('Progressive Dominion Rod') > 1" title="Dominion Rod" src="/img/twilight_princess/dominion.png" />
            <img v-else title="Dominion Rod (Broken)" src="/img/twilight_princess/brokendominion.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Dominion Rod')  }" />
            <img title="Fishing Rod" src="/img/twilight_princess/rod.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Fishing Rod')  }" />
            <img title="Bottle" src="/img/twilight_princess/bottle.png" :class="{ 'opacity-25': !hasBottle()  }" />
        </div>
    </div>
</template>
<script>
    /**
    * Twilight Princess
    *
    * Goal is to beat Ganondorf.
    * In order to beat him, you need :
    * - A Master Sword (sword level 3 or 4)
    * - 3 Fused Shadows
    * - The Shadow Crystal
    *
    */
    export default {
        name: "gDataTwilightPrincess",
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
                if (!this.data.slot_data.hasOwnProperty('rainbow_bridge'))
                    return [];
                var res = [];



                return res;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            closedSkyCity: function () {
                if (this.data.slot_data.hasOwnProperty('Settings') &&
                    (this.data.slot_data.Settings['City in the Sky Entrance Requirements'] == 'Yes')) {
                    return true;
                }
                return false;
            },
            closedPalaceOfTwilight: function () {
                if (this.data.slot_data.hasOwnProperty('Settings') &&
                    (this.data.slot_data.Settings['Palace of Twilight Requirements'] == 'Mirror Shards')) {
                    return true;
                }
                return false;
            },
            hasBottle: function () {
                if (this.$parent.getNumberItemsFromGroup(['Lantern Oil (Coro Bottle)', 'Milk (half) (Sera Bottle)', 'Empty Bottle (Fishing Hole)'])) {
                    return true;
                }
                return false;
            }
        },
        components: {
        },
    };
</script>
