<template>
    <div  class="inline-block">
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Badges</div>

            <img title="Boulder Badge" src="/img/pokemon_frlg/badges/boulder_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Boulder Badge')  }" />
            <img title="Cascade Badge" src="/img/pokemon_frlg/badges/cascade_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Cascade Badge')  }" />
            <img title="Thunder Badge" src="/img/pokemon_frlg/badges/thunder_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Thunder Badge')  }" />
            <img title="Rainbow Badge" src="/img/pokemon_frlg/badges/rainbow_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Rainbow Badge')  }" />
            <img title="Soul Badge" src="/img/pokemon_frlg/badges/soul_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Soul Badge')  }" />
            <img title="Marsh Badge" src="/img/pokemon_frlg/badges/marsh_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Marsh Badge')  }" />
            <img title="Volcano Badge" src="/img/pokemon_frlg/badges/volcano_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Volcano Badge')  }" />
            <img title="Earth Badge" src="/img/pokemon_frlg/badges/earth_badge.png" :class="{ 'opacity-25': !getNumberItemsFromName('Earth Badge')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">HMs</div>

            <img title="HM01 - Cut" src="/img/pokemon_frlg/hms/hm1.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM01 Cut')  }" />
            <img title="HM02 - Fly" src="/img/pokemon_frlg/hms/hm2.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM02 Fly')  }" />
            <img title="HM03 - Surf" src="/img/pokemon_frlg/hms/hm3.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM03 Surf')  }" />
            <img title="HM04 - Strength" src="/img/pokemon_frlg/hms/hm4.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM04 Strength')  }" />
            <img title="HM05 - Flash" src="/img/pokemon_frlg/hms/hm5.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM05 Flash')  }" />
            <img title="HM06 - Rock Smash" src="/img/pokemon_frlg/hms/hm6.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM06 Rock Smash')  }" />
            <img title="HM07 - Waterfall" src="/img/pokemon_frlg/hms/hm7.png" :class="{ 'opacity-25': !getNumberItemsFromName('HM07 Waterfall')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Key Items</div>

            <img v-if="itemfinderRequired()" title="Itemfinder" src="/img/pokemon_frlg/items/itemfinder.png" :class="{ 'opacity-25': !getNumberItemsFromName('Itemfinder')  }" />
            <img v-if="fameCheckerRequired()" title="Fame Checker" src="/img/pokemon_frlg/items/fame_checker.png" :class="{ 'opacity-25': !getNumberItemsFromName('Fame Checker')  }" />
            <img v-if="tmCaseShuffle()" title="TM Case" src="/img/pokemon_frlg/items/tm_case.png" :class="{ 'opacity-25': !getNumberItemsFromName('TM Case')  }" />

            <img v-if="superBicycle() && hasAccroBike()" title="Acrobatic Bicycle" src="/img/pokemon_frlg/items/acro_bike.png" />
            <img v-else title="Bicycle" src="/img/pokemon_frlg/items/bicycle.png" :class="{ 'opacity-25': !getNumberItemsFromName('Bicycle')  }" />
            <img v-if="jumpingShoes()" title="Jumping Shoes" src="/img/pokemon_frlg/items/jumping_shoes.png" :class="{ 'opacity-25': !getNumberItemsFromName('Jumping Shoes')  }" />


            <img v-if="oakParcel()" title="Oak's Parcel" src="/img/pokemon_frlg/items/oaks_parcel.png" :class="{ 'opacity-25': !getNumberItemsFromName('Oak\'s Parcel')  }" />
            <img title="S.S. Ticket" src="/img/pokemon_frlg/items/ss_ticket.png" :class="{ 'opacity-25': !getNumberItemsFromName('S.S. Ticket')  }" />
            <img title="Poke Flute" src="/img/pokemon_frlg/items/poke_flute.png" :class="{ 'opacity-25': !getNumberItemsFromName('Poke Flute')  }" />
            <img v-if="scopeRequired()" title="Silph Scope" src="/img/pokemon_frlg/items/silph_scope.png" :class="{ 'opacity-25': !getNumberItemsFromName('Silph Scope')  }" />
            <img v-if="extraKeyItems()" title="Hideout Key" src="/img/pokemon_frlg/items/hideout_key.png" :class="{ 'opacity-25': !getNumberItemsFromName('Hideout Key')  }" />
            <img v-if="extraKeyItems()" title="Safari Pass" src="/img/pokemon_frlg/items/safari_pass.png" :class="{ 'opacity-25': !getNumberItemsFromName('Safari Pass')  }" />
            <img v-if="extraKeyItems()" title="Machine Part" src="/img/pokemon_frlg/items/machine_part.png" :class="{ 'opacity-25': !getNumberItemsFromName('Machine Part')  }" />
            <img v-if="extraKeyItems()" title="Letter" src="/img/pokemon_frlg/items/letter.png" :class="{ 'opacity-25': !getNumberItemsFromName('Letter')  }" />
            <img v-if="!splitTea()" title="Tea" src="/img/pokemon_frlg/items/tea.png" :class="{ 'opacity-25': !getNumberItemsFromName('Tea')  }" />
            <span v-if="splitTea()" class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !$parent.getNumberItemsFromGroup(['Green Tea', 'Red Tea', 'Blue Tea', 'Purple Tea'])  }">
                <img title="Tea" src="/img/pokemon_frlg/items/tea.png" />x{{$parent.getNumberItemsFromGroup(['Green Tea', 'Red Tea', 'Blue Tea', 'Purple Tea'])}}
            </span>

            <img v-if="!splitCardKey()" title="Card Key" src="/img/pokemon_frlg/other/card_key.png" :class="{ 'opacity-25': !getNumberItemsFromName('Card Key')  }" />
            <span v-else class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !countCardKeys()  }"><img title="Card Key" src="/img/pokemon_frlg/items/card_key.png" />x{{countCardKeys()}}</span>

            <img v-if="!splitGymKey()" title="Secret Key" src="/img/pokemon_frlg/items/secret_key.png" :class="{ 'opacity-25': !getNumberItemsFromName('Secret Key')  }" />
            <span v-else class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !countGymKeys()  }"><img title="Gym Key" src="/img/pokemon_frlg/items/secret_key.png" />x{{countGymKeys()}}</span>

        </div>

        <div v-if="!kantoOnly()" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Sevii</div>

            <span v-if="splitSeviiPasses()" class="text-xs mr-1 font-bold" :class="{ 'opacity-25': !countSeviiPasses()  }"><img title="Island Pass" src="/img/pokemon_frlg/items/rainbow_pass.png" />x{{countSeviiPasses()}}</span>
            <span v-else>
                <img title="Tri Pass" src="/img/pokemon_frlg/items/tri_pass.png" :class="{ 'opacity-25': !getNumberItemsFromName('Tri Pass') && !getNumberItemsFromName('Progressive Pass') }" />
                <img title="Rainbow Pass" src="/img/pokemon_frlg/items/rainbow_pass.png" :class="{ 'opacity-25':  !getNumberItemsFromName('Rainbow Pass') && getNumberItemsFromName('Progressive Pass') < 2  }" />
            </span>
            <img v-if="roundTwo()" title="Ruby" src="/img/pokemon_frlg/items/ruby.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ruby')  }" />
            <img v-if="roundTwo()" title="Sapphire" src="/img/pokemon_frlg/items/sapphire.png" :class="{ 'opacity-25': !getNumberItemsFromName('Sapphire')  }" />
            <img title="Thank you for the Mystic Ticket !" src="/img/pokemon_frlg/items/mystic_ticket.png" :class="{ 'opacity-25': !getNumberItemsFromName('Mystic Ticket')  }" />

        </div>
    </div>
</template>
    
<script>

    /**
    * Pokemon FireRed and LeafGreen
    *
    * Goal is to beat Elite 4 (either Round 1 or 2).
    * You needs badges, like any other Pokemon game.
    * 
    */
export default {
  name: "gDataPokemonFRLG",
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
                var row_badges = { title: 'Badges required', value: null, details: null };
                var row_badges2 = { title: 'Badges required (R2)', value: null, details: null };

                if (this.data.slot_data.goal == 0) {
                    row_goal.value = 'Champion';
                    if (this.data.slot_data.elite_four_requirement == 1)
                        row_badges.title = 'Gyms to vainquish';
                    row_badges.value = this.data.slot_data.elite_four_count;
                }
                else if (this.data.slot_data.goal == 1) {
                    row_goal.value = 'Champion Rematch';
                    row_badges.title = 'Badges required (R1)';
                    if (this.data.slot_data.elite_four_requirement == 1)
                        row_badges.title = 'Gyms to vainquish (R1)';
                    row_badges.value = this.data.slot_data.elite_four_count;
                    if (this.data.slot_data.elite_four_rematch_requirement == 1)
                        row_badges2.title = 'Gyms to vainquish (R2)';
                    row_badges2.value = this.data.slot_data.elite_four_rematch_count;
                }

                res.push(row_goal);
                if (row_badges.value)
                    res.push(row_badges);
                if (row_badges2.value)
                    res.push(row_badges2);

                // Viridian Gym
                var row_tmp = { title: 'Viridian Gym requirment', value: null, details: null };
                if (this.data.slot_data.viridian_gym_requirement) {
                    if (this.data.slot_data.viridian_gym_count > 1)
                        row_tmp.value = this.data.slot_data.viridian_gym_count + ' gyms';
                    else if (this.data.slot_data.viridian_gym_count)
                        row_tmp.value = this.data.slot_data.viridian_gym_count + ' gym';
                }
                else {
                    if (this.data.slot_data.viridian_gym_count > 1)
                        row_tmp.value = this.data.slot_data.viridian_gym_count + ' badges';
                    else if (this.data.slot_data.viridian_gym_count)
                        row_tmp.value = this.data.slot_data.viridian_gym_count + ' badge';
                }
                if (row_tmp.value)
                    res.push(row_tmp);

                // Cerulean Cave
                var row_tmp = { title: 'Cerulean Cave requirment', value: null, details: null };
                if (this.data.slot_data.cerulean_cave_requirement) {
                    if (this.data.slot_data.cerulean_cave_count > 1)
                        row_tmp.value = this.data.slot_data.cerulean_cave_count + ' gyms';
                    else if (this.data.slot_data.cerulean_cave_count)
                        row_tmp.value = this.data.slot_data.cerulean_cave_count + ' gym';
                }
                else {
                    if (this.data.slot_data.cerulean_cave_count > 1)
                        row_tmp.value = this.data.slot_data.cerulean_cave_count + ' badges';
                    else if (this.data.slot_data.cerulean_cave_count)
                        row_tmp.value = this.data.slot_data.cerulean_cave_count + ' badge';
                }
                if (row_tmp.value)
                    res.push(row_tmp);

                var row_roadblocks = { title: 'World update', value: null, details: null };
                if (this.data.slot_data.modify_world_state && this.data.slot_data.modify_world_state.length) {
                    row_roadblocks.value = this.data.slot_data.modify_world_state.join(', ');
                    res.push(row_roadblocks);
                }
                row_roadblocks = { title: 'Remove Badge requirment', value: null, details: null };
                if (this.data.slot_data.remove_badge_requirement.length) {
                    row_roadblocks.value = this.data.slot_data.remove_badge_requirement.join(', ');
                    res.push(row_roadblocks);
                }

                var row_pkmn = { title: 'Caught number for Oak\'s aide', value: 0, details: null };
                var settings = ['oaks_aide_route_2', 'oaks_aide_route_10', 'oaks_aide_route_11', 'oaks_aide_route_15', 'oaks_aide_route_16'];
                for (var x = 0; x < settings.length; x++) {
                    if (this.data.slot_data[settings[x]] > row_pkmn.value)
                        row_pkmn.value = this.data.slot_data[settings[x]];
                }
                if (row_pkmn.value > 0) {
                    res.push(row_pkmn);
                }

                return res;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            countSeviiPasses: function (name) {
                return this.$parent.getNumberItemsFromGroup(['One Pass', 'Two Pass', 'Three Pass', 'Four Pass', 'Five Pass', 'Six Pass', 'Seven Pass']);
            },
            countGymKeys: function (name) {
                return this.$parent.getNumberItemsFromGroup(['Cinnabar Key', 'Saffron Key', 'Viridian Key', 'Pewter Key', 'Cerulean Key', 'Celadon Key', 'Fuchsia Key', 'Vermilion Key']);
            },
            countCardKeys: function () {
                return this.$parent.getNumberItemsFromName('Progressive Card Key') + this.$parent.getNumberItemsNameStart('Card Key');
            }, 
            scopeRequired: function () {
                if (this.data.slot_data.hasOwnProperty('modify_world_state')) {
                    return !this.data.slot_data.modify_world_state.includes('Open Silph') || this.data.slot_data.modify_world_state.includes('Block Tower');
                }
                return false;
            },
            roundTwo: function () {
                if (this.data.slot_data.hasOwnProperty('goal')) {
                    return this.data.slot_data.goal;
                }
                return 1;
            },
            kantoOnly: function () {
                if (this.data.slot_data.hasOwnProperty('kanto_only')) {
                    return this.data.slot_data.kanto_only;
                }
                return 0;
            },
            tmCaseShuffle: function () {
                if (this.data.slot_data.hasOwnProperty('shuffle_tm_case')) {
                    return this.data.slot_data.shuffle_tm_case;
                }
                return 0;
            }, 
            fameCheckerRequired: function () {
                if (this.data.slot_data.hasOwnProperty('fame_checker_required') && this.data.slot_data.hasOwnProperty('famesanity')) {
                    return this.data.slot_data.fame_checker_required && this.data.slot_data.famesanity;
                }
                return 1;
            },
            itemfinderRequired: function () {
                if (this.data.slot_data.hasOwnProperty('itemfinder_required')) {
                    return this.data.slot_data.itemfinder_required;
                }
                return 1;
            },
            splitTea: function () {
                if (this.data.slot_data.hasOwnProperty('split_teas')) {
                    return this.data.slot_data.split_teas;
                }
                return 0;
            },
            splitCardKey: function () {
                if (this.data.slot_data.hasOwnProperty('card_key')) {
                    return this.data.slot_data.card_key;
                }
                return 0;
            },
            splitGymKey: function () {
                if (this.data.slot_data.hasOwnProperty('gym_keys')) {
                    return this.data.slot_data.gym_keys;
                }
                return 0;
            },
            extraKeyItems: function () {
                if (this.data.slot_data.hasOwnProperty('extra_key_items')) {
                    return this.data.slot_data.extra_key_items;
                }
                return this.$parent.getNumberItemsFromGroup(['Hideout Key', 'Letter', 'Safari Pass', 'Machine Part']);
            },
            superBicycle: function () {
                if (this.data.slot_data.hasOwnProperty('acrobatic_bicycle')) {
                    return this.data.slot_data.acrobatic_bicycle;
                }
                return this.hasAccroBike();
            },
            hasAccroBike: function () {
                if (this.getNumberItemsFromName('Bicycle')) {
                    if (this.data.slot_data.hasOwnProperty('bicycle_requires_jumping_shoes') && this.data.slot_data.bicycle_requires_jumping_shoes && this.data.slot_data.shuffle_jumping_shoes && !this.getNumberItemsFromName('Jumping Shoes'))
                        return 0;
                    return 1;
                }
                return 0;
            },
            jumpingShoes: function () {
                if (this.data.slot_data.hasOwnProperty('shuffle_jumping_shoes')) {
                    return this.data.slot_data.shuffle_jumping_shoes;
                }
                return this.getNumberItemsFromName('Jumping Shoes');
            },
            oakParcel: function () {
                if (this.data.slot_data.hasOwnProperty('viridian_city_roadblock')) {
                    return this.data.slot_data.viridian_city_roadblock;
                }
                return this.getNumberItemsFromName('Oak\'s Parcel');
            },
            splitSeviiPasses: function () {
                if (this.data.slot_data.hasOwnProperty('island_passes')) {
                    return this.data.slot_data.island_passes > 1;
                }
                return this.countSeviiPasses();
            },
        },
  components: {
  },
};
</script>
