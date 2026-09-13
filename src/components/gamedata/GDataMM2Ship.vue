<template>
    <div class="inline-block">
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Rewards</div>

            <img title="Odolwa's Remains" src="/img/mm/equipment/odolwa.png" :class="{ 'opacity-25': !getNumberItemsFromName('Odolwa\'s Remains')  }" />
            <img title="Goht's Remains" src="/img/mm/equipment/goht.png" :class="{ 'opacity-25': !getNumberItemsFromName('Goht\'s Remains')  }" />
            <img title="Gyorg's Remains" src="/img/mm/equipment/gyorg.png" :class="{ 'opacity-25': !getNumberItemsFromName('Gyorg\'s Remains')  }" />
            <img title="Twinmold's Remains" src="/img/mm/equipment/twinmold.png" :class="{ 'opacity-25': !getNumberItemsFromName('Twinmold\'s Remains')  }" />
            <span class="mr-2"></span>
            <img title="Oath to Order" src="/img/mm/equipment/song_oath.png" :class="{ 'opacity-25': !getNumberItemsFromName('Oath to Order')  }" />
            <span v-if="getClockShuffle()" class="mr-2"></span>
            <img v-if="getClockShuffle()" title="Time (Day 1)" src="/img/mm/Clock_Day.png" :class="{ 'opacity-25': !getClockItem(0)  }" />
            <img v-if="getClockShuffle()" title="Night (Night 1)" src="/img/mm/Clock_Night.png" :class="{ 'opacity-25': !getClockItem(1)  }" />
            <img v-if="getClockShuffle()" title="Time (Day 2)" src="/img/mm/Clock_Day.png" :class="{ 'opacity-25': !getClockItem(2)  }" />
            <img v-if="getClockShuffle()" title="Night (Night 2)" src="/img/mm/Clock_Night.png" :class="{ 'opacity-25': !getClockItem(3)  }" />
            <img v-if="getClockShuffle()" title="Time (Day 3)" src="/img/mm/Clock_Day.png" :class="{ 'opacity-25': !getClockItem(4)  }" />
            <img v-if="getClockShuffle()" title="Night (Night 3)" src="/img/mm/Clock_Night.png" :class="{ 'opacity-25': !getClockItem(5)  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Inventory</div>

            <img v-if="getSwordLevel() > 2" title="Gilded Sword" src="/img/mm/equipment/sword3.png" />
            <img v-else-if="getSwordLevel() > 1" title="Razor Sword" src="/img/mm/equipment/sword2.png" />
            <img v-else title="Kokiri Sword" src="/img/mm/equipment/sword1.png" :class="{ 'opacity-25': !getSwordLevel()  }" />

            <img v-if="getShieldLevel() > 1" title="Mirror Shield" src="/img/mm/equipment/shield2.png" />
            <img v-else title="Hero's Shield" src="/img/mm/equipment/shield1.png" :class="{ 'opacity-25': !getShieldLevel()  }" />

            <img v-if="getNumberItemsFromName('Progressive Magic') > 1" title="Magic" src="/img/mm/equipment/magic2.png" />
            <img v-else src="/img/mm/equipment/magic1.png" title="Magic" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Magic')  }" />

            <img title="Ocarina of Time" src="/img/mm/items/ocarina.png" />
            <img v-if="getNumberItemsFromName('Progressive Bomb Bag')" title="Bomb Bag" src="/img/mm/items/bomb.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Bombchu')" title="Bombchus" src="/img/mm/items/bombchu.png" />
            <img v-else-if="getNumberItemsFromName('Blask Mask')" title="Blast Mask" src="/img/mm/masks/blast.png" />
            <img title="Explosives" v-else src="/img/mm/items/bomb.png" class="opacity-25" />
            <img title="Bow" src="/img/mm/items/bow.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Bow')  }" />
            <img title="Fire Arrow" src="/img/mm/items/fire_arrow.png" :class="{ 'opacity-25': !getNumberItemsFromName('Fire Arrow')  }" />
            <img title="Ice Arrow" src="/img/mm/items/ice_arrow.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ice Arrow')  }" />
            <img title="Light Arrow" src="/img/mm/items/light_arrow.png" :class="{ 'opacity-25': !getNumberItemsFromName('Light Arrow')  }" />
            <img title="Hookshot" src="/img/mm/items/hookshot.png" :class="{ 'opacity-25': !getNumberItemsFromName('Hookshot')  }" />
            <img title="Pictograph Box" src="/img/mm/items/pictobox.png" :class="{ 'opacity-25': !getNumberItemsFromName('Pictograph Box')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Masks</div>

            <img title="Deku Mask" src="/img/mm/masks/deku_mask.png" :class="{ 'opacity-25': !getNumberItemsFromName('Deku Mask')  }" />
            <img title="Goron Mask" src="/img/mm/masks/goron.png" :class="{ 'opacity-25': !getNumberItemsFromName('Goron Mask')  }" />
            <img title="Zora Mask" src="/img/mm/masks/zora.png" :class="{ 'opacity-25': !getNumberItemsFromName('Zora Mask')  }" />
            <img title="Fierce Deity's Mask" src="/img/mm/masks/fierce_deity.png" :class="{ 'opacity-25': !getNumberItemsFromName('Fierce Deity\'s Mask')  }" />
            <img title="Great Fairy Mask" src="/img/mm/masks/fairy_mask.png" :class="{ 'opacity-25': !getNumberItemsFromName('Great Fairy Mask')  }" />
            <img title="Gibdo Mask" src="/img/mm/masks/captains.png" :class="{ 'opacity-25': !getNumberItemsFromName('Captain\'s Hat')  }" />
            <img title="Garo Mask" src="/img/mm/masks/garo_mask.png" :class="{ 'opacity-25': !getNumberItemsFromName('Garo Mask')  }" />
            <img title="Gibdo Mask" src="/img/mm/masks/gibdo.png" :class="{ 'opacity-25': !getNumberItemsFromName('Gibdo Mask')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Songs</div>

            <img title="Song of Time" src="/img/mm/equipment/song_time.png" :class="{ 'opacity-25': !getNumberItemsFromName('Song of Time')  }" />
            <img title="Epona's Song" src="/img/mm/equipment/song_epona.png" :class="{ 'opacity-25': !getNumberItemsFromName('Epona\'s Song')  }" />
            <img title="Song of Healing" src="/img/mm/equipment/song_healing.png" :class="{ 'opacity-25': !getNumberItemsFromName('Song of Healing')  }" />
            <img title="Song of Soaring" src="/img/mm/equipment/song_soaring.png" :class="{ 'opacity-25': !getNumberItemsFromName('Song of Soaring')  }" />
            <img title="Song of Storms" src="/img/mm/equipment/song_storms.png" :class="{ 'opacity-25': !getNumberItemsFromName('Song of Storms')  }" />
            <img title="Sonata of Awakening" src="/img/mm/equipment/song_sonata.png" :class="{ 'opacity-25': !getNumberItemsFromName('Sonata of Awakening')  }" />
            <img title="Goron's Lullaby" src="/img/mm/equipment/song_lullaby.png" :class="{ 'opacity-25': getNumberItemsFromName('Progressive Goron Lullaby') < 2 }" />
            <img title="New Wave Bossa Nova" src="/img/mm/equipment/song_bossa_nova.png" :class="{ 'opacity-25': !getNumberItemsFromName('New Wave Bossa Nova')  }" />
            <img title="Elegy of Emptiness" src="/img/mm/equipment/song_elegy.png" :class="{ 'opacity-25': !getNumberItemsFromName('Elegy of Emptiness')  }" />
        </div>
    </div>
</template>
    
<script>


    /**
    * Majora's Mask Recompiled
    * 
    * Goal is to get bosses remains.
    */ 
export default {
        name: "gDataMajorasMask",
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
                var row_majora = { title: 'Remains needed for Majora', value: this.data.slot_data.access_majora_remains_count, details: null };
                var row_moon = { title: 'Remains needed for the moon', value: this.data.slot_data.access_moon_remains_count, details: null };


                res.push(row_majora);
                res.push(row_moon);

                var row_fairies = { title: 'Fairies required for Great Rewards', value: this.data.slot_data.stray_fairies_required, details: null };
                var row_skultullas = { title: 'Skultullas tokens required to uncurse', value: this.data.slot_data.skulltula_tokens_required, details: null };

                res.push(row_fairies);
                res.push(row_skultullas);


                var row_starting_time = { title: 'Starting Clock', value: this.data.slot_data.starting_clock, details: null };

                if (this.data.slot_data.starting_clock != "")
                    res.push(row_starting_time);

                var dlcs = []; 
                if (this.data.slot_data.placement_small_keys == 0)
                    dlcs.push('Small Keys');
                if (this.data.slot_data.placement_boss_keys == 0)
                    dlcs.push('Boss Keys');
                if (this.data.slot_data.placement_stray_fairies == 0)
                    dlcs.push('Stray Fairies');
                if (this.data.slot_data.shuffle_gold_skulltulas == 1)
                    dlcs.push('Skultullas Tokens');
                if (this.data.slot_data.shuffle_cows == 1)
                    dlcs.push('Cows');
                if (this.data.slot_data.shuffle_frogs == 1)
                    dlcs.push('Frogs');
                if (this.data.slot_data.shuffle_shops > 1)
                    dlcs.push('Shops');
                if (this.data.slot_data.shuffle_freestanding_items == 1)
                    dlcs.push('Freestanding Items');
                if (this.data.slot_data.shuffle_crate_drops == 1)
                    dlcs.push('Crates');
                if (this.data.slot_data.shuffle_barrel_drops == 1)
                    dlcs.push('Barrels');
                if (this.data.slot_data.shuffle_pot_drops == 1)
                    dlcs.push('Pots');
                if (this.data.slot_data.shuffle_grass_drops == 1)
                    dlcs.push('Grass');
                if (this.data.slot_data.shuffle_hive_drops == 1)
                    dlcs.push('Beehives');
                if (this.data.slot_data.shuffle_snowball_drops == 1)
                    dlcs.push('Snowballs');
                if (this.data.slot_data.shuffle_wonder_items == 1)
                    dlcs.push('Wonder Items');
                if (this.data.slot_data.shuffle_tree_drops == 1)
                    dlcs.push('Trees');
                if (this.data.slot_data.shuffle_enemy_drops == 1)
                    dlcs.push('Enemy Drops');
                if (this.data.slot_data.shuffle_butterflies == 1)
                    dlcs.push('Butterflies');
                if (this.data.slot_data.curiostity_shop_trades == 1)
                    dlcs.push('Shop Trades');
                if (this.data.slot_data.shuffle_owl_statues == 1)
                    dlcs.push('Owl Statues');
                if (this.data.slot_data.shuffle_enemy_souls == 1)
                    dlcs.push('Enemy Souls');
                if (this.data.slot_data.shuffle_boss_souls == 1)
                    dlcs.push('Boss Souls');

                var row_dlc = { title: 'Extra Shuffle', value: null, details: null };
                if (dlcs.length) {
                    row_dlc.value = dlcs.join(', ');
                    res.push(row_dlc);
                }
                return res;
            },
            getClockShuffle: function () {
                if (!this.$parent.hasSlotData())
                    return 0;
                return this.data.slot_data.clock_shuffle;
            },
            getClockItem: function (number) {
                if (!this.$parent.hasSlotData())
                    return 1;

                const clock_arrays = ['Time (Day 1)', 'Time (Night 1)', 'Time (Day 2)', 'Time (Night 2)', 'Time (Day 3)', 'Time (Night 3)'];

                // En attendant d'avoir l'inventaire de départ.
                if (this.$parent.hasSlotData() && this.data.slot_data.starting_clock == clock_arrays[number])
                    return true;

                if (this.data.slot_data.clock_shuffle == 1) {
                    if (!this.data.slot_data.clock_shuffle_progressive)
                        return this.getNumberItemsFromName(clock_arrays[number]);
                    else if (this.data.slot_data.clock_shuffle_progressive == 1)
                        return this.getNumberItemsFromName('Progressive Time') > number ? 1 : 0;

                    return this.getNumberItemsFromName('Progressive Time') > (5 - number) ? 1 : 0;
                }

                return 1;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            getSwordLevel: function () {
                var res = 1;
                if (this.data.slot_data.shuffle_sword) {
                    res -= 1;
                }
                return res + this.getNumberItemsFromName('Progressive Sword');
            },
            getShieldLevel: function () {
                var res = 1;
                if (this.data.slot_data.shuffle_shield) {
                    res -= 1;
                }
                return res + this.getNumberItemsFromName('Progressive Shield');
            }
        },
  components: {
  },
};
</script>
