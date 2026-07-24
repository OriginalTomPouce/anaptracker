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
            <img title="Kafei's Mask" src="/img/mm/masks/kafei_mask.png" :class="{ 'opacity-25': !getNumberItemsFromName('Kafei\'s Mask')  }" />
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
            <img title="Goron's Lullaby" src="/img/mm/equipment/song_lullaby.png" :class="{ 'opacity-25': !getNumberItemsFromName('Goron Lullaby')  }" />
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
                var row_majora = { title: 'Remains needed for Majora', value: this.data.slot_data.majora_remains_required, details: null };
                var row_moon = { title: 'Remains needed for the moon', value: this.data.slot_data.moon_remains_required, details: null };


                res.push(row_majora);
                res.push(row_moon);

                var row_fairies = { title: 'Fairies required for Great Rewards', value: this.data.slot_data.required_stray_fairies, details: null };
                var row_skultullas = { title: 'Skultullas tokens required to uncurse', value: this.data.slot_data.required_skull_tokens, details: null };

                res.push(row_fairies);
                res.push(row_skultullas);

                var dlcs = []; 
                if (this.data.slot_data.keysanity == 1)
                    dlcs.push('Small Keys');
                if (this.data.slot_data.bosskeysanity == 1)
                    dlcs.push('Boss Keys');
                if (this.data.slot_data.fairysanity == 1)
                    dlcs.push('Stray Fairies');
                if (this.data.slot_data.skullsanity == 1)
                    dlcs.push('Skultullas Tokens');
                if (this.data.slot_data.scrubsanity == 1)
                    dlcs.push('Scrubs');
                if (this.data.slot_data.cowsanity == 1)
                    dlcs.push('Cows');
                if (this.data.slot_data.shopsanity > 1)
                    dlcs.push('Shops');
                if (this.data.slot_data.curiostity_shop_trades == 1)
                    dlcs.push('Shop Trades');


                var row_dlc = { title: 'Extra Shuffle', value: null, details: null };
                if (dlcs.length) {
                    row_dlc.value = dlcs.join(', ');
                    res.push(row_dlc);
                }
                return res;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            getSwordLevel: function () {
                var res = 1;
                if (this.data.slot_data.swordless) {
                    res -= 1;
                }
                return res + this.getNumberItemsFromName('Progressive Sword');
            },
            getShieldLevel: function () {
                var res = 1;
                if (this.data.slot_data.shieldless) {
                    res -= 1;
                }
                return res + this.getNumberItemsFromName('Progressive Shield');
            }
        },
  components: {
  },
};
</script>
