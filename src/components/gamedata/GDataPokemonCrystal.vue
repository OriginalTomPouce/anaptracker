<template>
    <div class="inline-block">

        <div v-if="unownGoal()" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Tiles</div>

            <span v-if="unownGoal()" class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Kabuto Tile')  }"><img title="Kabuto Tile" src="/img/pokemon_crystal/items/KABUTO_TILE.png" />x{{getNumberItemsFromName('Kabuto Tile')}}</span>
            <span v-if="unownGoal()" class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Omanyte Tile')  }"><img title="Omanyte Tile" src="/img/pokemon_crystal/items/OMANYTE_TILE.png" />x{{getNumberItemsFromName('Omanyte Tile')}}</span>
            <span v-if="unownGoal()" class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Aerodactyl Tile')  }"><img title="Aerodactyl Tile" src="/img/pokemon_crystal/items/AERODACTYL_TILE.png" />x{{getNumberItemsFromName('Aerodactyl Tile')}}</span>
            <span v-if="unownGoal()" class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Ho-Oh Tile')  }"><img title="Ho-Oh Tile" src="/img/pokemon_crystal/items/HO-OH_TILE.png" />x{{getNumberItemsFromName('Ho-Oh Tile')}}</span>
        </div>
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Badges</div>


            <img title="Zephyr Badge" src="/img/pokemon_crystal/items/zephyrbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Zephyr Badge')  }" />
            <img title="Hive Badge" src="/img/pokemon_crystal/items/hivebadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Hive Badge')  }" />
            <img title="Plain Badge" src="/img/pokemon_crystal/items/plainbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Plain Badge')  }" />
            <img title="Fog Badge" src="/img/pokemon_crystal/items/fogbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Fog Badge')  }" />
            <img title="Storm Badge" src="/img/pokemon_crystal/items/stormbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Storm Badge')  }" />
            <img title="Mineral Badge" src="/img/pokemon_crystal/items/mineralbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Mineral Badge')  }" />
            <img title="Glacier Badge" src="/img/pokemon_crystal/items/glacierbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Glacier Badge')  }" />
            <img title="Rising Badge" src="/img/pokemon_crystal/items/risingbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Rising Badge')  }" />
            <span v-if="kantoIsOn()" class="mr-2"></span>
            <img v-if="kantoIsOn()" title="Boulder Badge" src="/img/pokemon_crystal/items/boulderbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Boulder Badge')  }" />
            <img v-if="kantoIsOn()" title="Cascade Badge" src="/img/pokemon_crystal/items/cascadebadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Cascade Badge')  }" />
            <img v-if="kantoIsOn()" title="Thunder Badge" src="/img/pokemon_crystal/items/thunderbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Thunder Badge')  }" />
            <img v-if="kantoIsOn()" title="Rainbow Badge" src="/img/pokemon_crystal/items/rainbowbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Rainbow Badge')  }" />
            <img v-if="kantoIsOn()" title="Soul Badge" src="/img/pokemon_crystal/items/soulbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Soul Badge')  }" />
            <img v-if="kantoIsOn()" title="Marsh Badge" src="/img/pokemon_crystal/items/marshbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Marsh Badge')  }" />
            <img v-if="kantoIsOn()" title="Volcano Badge" src="/img/pokemon_crystal/items/volcanobadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Volcano Badge')  }" />
            <img v-if="kantoIsOn()" title="Earth Badge" src="/img/pokemon_crystal/items/earthbadge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Earth Badge')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">HMs</div>

            <img title="HM01 - Cut" src="/img/pokemon_crystal/items/hm01.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM01 Cut')  }" />
            <img title="HM02 - Fly" src="/img/pokemon_crystal/items/hm02.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM02 Fly')  }" />
            <img title="HM03 - Surf" src="/img/pokemon_crystal/items/hm03.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM03 Surf')  }" />
            <img title="HM04 - Strength" src="/img/pokemon_crystal/items/hm04.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM04 Strength')  }" />
            <img title="HM05 - Flash" src="/img/pokemon_crystal/items/hm05.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM05 Flash')  }" />
            <img title="HM06 - Whirlpool" src="/img/pokemon_crystal/items/hm06.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM06 Whirlpool')  }" />
            <img title="HM07 - Waterfall" src="/img/pokemon_crystal/items/hm07.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM07 Waterfall')  }" />
            <img title="TM08 - Rock Smash" src="/img/pokemon_crystal/items/tm08.png" :class="{ 'opacity-25': !getNumberItemsFromName('TM08')  }" />
        </div>
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Key Items</div>
            
            <img v-if="dexsanityTracking()" title="Pokedex" src="/img/pokemon_crystal/items/pokedex.png" :class="{ 'opacity-25': !getNumberItemsFromName('Pokedex')  }" />
            <img v-if="itemfinderRequired()" title="Itemfinder" src="/img/pokemon_crystal/items/itemfinder.png" :class="{ 'opacity-25': !getNumberItemsFromName('Itemfinder')  }" />
            <img v-if="!getNumberItemsFromName('Pokegear')" src="/img/pokemon_crystal/items/pokegear.png" title="Pokegear" class="opacity-25" />
            <img v-else-if="!getNumberItemsFromName('Radio Card')" src="/img/pokemon_crystal/items/pokegear.png" title="Pokegear" />
            <img v-else-if="!getNumberItemsFromName('EXPN Card')" title="Radio Card" src="/img/pokemon_crystal/items/radiocard.png" />
            <img v-else title="EXPN. Card" src="/img/pokemon_crystal/items/expncard.png" />
            <img title="Bicycle" src="/img/pokemon_crystal/items/bicycle.png" :class="{ 'opacity-25': !getNumberItemsFromName('Bicycle')  }" />
            <img title="Squirtbottle" src="/img/pokemon_crystal/items/squirtbottle.png" :class="{ 'opacity-25': !getNumberItemsFromName('Squirtbottle')  }" />
            <img v-if="kantoIsOn()" title="S.S. Ticket" src="/img/pokemon_crystal/items/ssticket.png" :class="{ 'opacity-25': !getNumberItemsFromName('S.S. Ticket')  }" />
            <img v-if="kantoIsOn()" title="Pass" src="/img/pokemon_crystal/items/pass.png" :class="{ 'opacity-25': !getNumberItemsFromName('Pass')  }" />
            <img title="Basement Key" src="/img/pokemon_crystal/items/basementkey.png" :class="{ 'opacity-25': !getNumberItemsFromName('Basement Key')  }" />
            <img title="Card Key" src="/img/pokemon_crystal/items/cardkey.png" :class="{ 'opacity-25': !getNumberItemsFromName('Card Key')  }" />
            <img v-if="!getNumberItemsFromName('Clear Bell')" title="Clear Bell" src="/img/pokemon_crystal/items/clearbell.png" class="opacity-25" />
            <img v-else-if="!getNumberItemsFromName('Rainbow Wing')" title="Clear Bell" src="/img/pokemon_crystal/items/clearbell.png" />
            <img v-else title="Rainbow Wing" src="/img/pokemon_crystal/items/rainbowwing.png" />
            <img v-if="kantoIsOn() && teaIsOn()" title="Tea" src="/img/pokemon_crystal/items/tea.png" :class="{ 'opacity-25': !getNumberItemsFromName('Tea')  }" />
            <img v-if="kantoIsOn()" title="Machine Part" src="/img/pokemon_crystal/items/machinepart.png" :class="{ 'opacity-25': !getNumberItemsFromName('Machine Part')  }" />
        </div>
    </div>
</template>
    
<script>

    /**
    * Pokemon Crystal
    *
    * Goal is to either beat Red or be League Champion.
    * It either needs badges or gyms. But we can assume badges are required because they can also lock areas (Pokemon League, Mt Silver, Team Rocket invasion, ...)
    */
export default {
  name: "gDataPokemonCrystal",
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
                if (!this.$parent.hasSlotData())
                    return [];
                var res = [];
                var row_goal = { title: 'Goal', value: null, details: null };

                row_goal.value = this.data.slot_data.goal.join(', ');

                res.push(row_goal);

                // Areas Locked

                // Mt Silver
                var row_tmp = { title: 'Mt. Silver requirement', value: null, details: null };
                if (this.data.slot_data.mt_silver_requirement) {
                    if (this.data.slot_data.mt_silver_count > 1)
                        row_tmp.value = this.data.slot_data.mt_silver_count + ' gyms';
                    else if (this.data.slot_data.mt_silver_count)
                        row_tmp.value = this.data.slot_data.mt_silver_count + ' gym';
                }
                else {
                    if (this.data.slot_data.mt_silver_count > 1)
                        row_tmp.value = this.data.slot_data.mt_silver_count + ' badges';
                    else if (this.data.slot_data.mt_silver_count)
                        row_tmp.value = this.data.slot_data.mt_silver_count + ' badge';
                }
                if (row_tmp.value)
                    res.push(row_tmp);


                // Team Rocket invasion
                row_tmp = { title: 'Radio Tower requirement', value: null, details: null };
                if (this.data.slot_data.radio_tower_requirement) {
                    if (this.data.slot_data.radio_tower_count > 1)
                        row_tmp.value = this.data.slot_data.radio_tower_count + ' gyms';
                    else if (this.data.slot_data.radio_tower_count)
                        row_tmp.value = this.data.slot_data.radio_tower_count + ' gym';
                }
                else {
                    if (this.data.slot_data.radio_tower_count > 1)
                        row_tmp.value = this.data.slot_data.radio_tower_count + ' badges';
                    else if (this.data.slot_data.radio_tower_count)
                        row_tmp.value = this.data.slot_data.radio_tower_count + ' badge';
                }
                if (row_tmp.value)
                    res.push(row_tmp);

                // Victory Road
                row_tmp = { title: 'Victory Road requirement', value: null, details: null };
                if (this.data.slot_data.elite_four_requirement) {
                    if (this.data.slot_data.elite_four_count > 1)
                        row_tmp.value = this.data.slot_data.elite_four_count + ' gyms';
                    else if (this.data.slot_data.elite_four_count)
                        row_tmp.value = this.data.slot_data.elite_four_count + ' gym';
                }
                else {
                    if (this.data.slot_data.elite_four_count > 1)
                        row_tmp.value = this.data.slot_data.elite_four_count + ' badges';
                    else if (this.data.slot_data.elite_four_count)
                        row_tmp.value = this.data.slot_data.elite_four_count + ' badge';
                }
                if (row_tmp.value)
                    res.push(row_tmp);


                // Route 44
                row_tmp = { title: 'Route 44 requirement', value: null, details: null };
                if (this.data.slot_data.route_44_access_requirement) {
                    if (this.data.slot_data.route_44_access_count > 1)
                        row_tmp.value = this.data.slot_data.route_44_access_count + ' gyms';
                    else if (this.data.slot_data.route_44_access_count)
                        row_tmp.value = this.data.slot_data.route_44_access_count + ' gym';
                }
                else {
                    if (this.data.slot_data.route_44_access_count > 1)
                        row_tmp.value = this.data.slot_data.route_44_access_count + ' badges';
                    else if (this.data.slot_data.route_44_access_count)
                        row_tmp.value = this.data.slot_data.route_44_access_count + ' badge';
                }
                if (row_tmp.value)
                    res.push(row_tmp);

                if (this.data.slot_data.enable_mischief)
                    res.push({ title: '\'v\'', value: null, details: null });

                return res;
            },
            dexsanityTracking: function () {
                if (this.data.slot_data.hasOwnProperty('dexsanity') && (this.data.slot_data.dexsanity > 0 || this.data.slot_data.dexcountsanity_checks > 0) && this.data.slot_data.randomize_pokedex == 2) {
                    return 1;
                }
                return 0;
            }, 
            itemfinderRequired: function () {
                if (this.data.slot_data.hasOwnProperty('require_itemfinder')) {
                    return this.data.slot_data.require_itemfinder;
                }
                return 1;
            }, 
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            teaIsOn: function () {
                if (this.data.slot_data.hasOwnProperty('tea_east') && this.data.slot_data.tea_east == 0 && this.data.slot_data.tea_west == 0 && this.data.slot_data.tea_north == 0 && this.data.slot_data.tea_south == 0) {
                    return 0;
                }

                    return 1;
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            kantoIsOn: function () {
                if (this.data.slot_data.hasOwnProperty('johto_only') && this.data.slot_data.johto_only == 1)
                    return false;
                return true;
            },
            unownGoal: function () {
                if (this.data.slot_data.hasOwnProperty('goal')) {
                    if (this.data.slot_data.goal.contains("Unown Hunt"))
                        return true;
                    return false;

                }
                return this.getNumberItemsFromName('Omanyte Tile') + this.getNumberItemsFromName('Aerodactyl Tile') + this.getNumberItemsFromName('Ho-Oh Tile') + this.getNumberItemsFromName('Kabuto Tile');
            }
        },
  components: {
  },
};
</script>
