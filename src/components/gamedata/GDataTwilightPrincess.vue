<template>
    <div class="inline-block">
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>
            <span v-if="triforceHunt()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Triforce Piece')  }"><img title="Triforce Piece" src="/img/oot/triforce.png" />x{{ getNumberItemsFromName('Triforce Piece') }} </span> / {{ triforceHunt() }}</span>

            <span v-if="skullsTokensCounts()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Gold Skulltula Token')  }"><img title="Gold Skulltulla Token" src="/img/oot/skull.png" />x{{ getNumberItemsFromName('Gold Skulltula Token') }} </span> / {{ skullsTokensCounts() }}</span>
            <img title="Kokiri's Emerald" v-if="stonesCounts()" src="/img/oot/stone_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Kokiri\'s Emerald')  }" />
            <img title="Goron's Ruby" v-if="stonesCounts()" src="/img/oot/stone_2.png" :class="{ 'opacity-25': !getNumberItemsFromName('Goron\'s Ruby')  }" />
            <img title="Zora's Sapphire" v-if="stonesCounts()" src="/img/oot/stone_3.png" :class="{ 'opacity-25': !getNumberItemsFromName('Zora\'s Sapphire')  }" />
            <img title="Forest Medaillon" v-if="medalsCounts()" src="/img/oot/medal_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Forest Medallion')  }" />
            <img title="Fire Medaillin" v-if="medalsCounts()" src="/img/oot/medal_2.png" :class="{ 'opacity-25': !getNumberItemsFromName('Fire Medallion')  }" />
            <img title="Water Medaillon" v-if="medalsCounts()" src="/img/oot/medal_3.png" :class="{ 'opacity-25': !getNumberItemsFromName('Water Medallion')  }" />
            <img title="Shadow Medaillon" v-if="LACSCounts()" src="/img/oot/medal_4.png" :class="{ 'opacity-25': !getNumberItemsFromName('Shadow Medallion')  }" />
            <img title="Spirit Medaillon" v-if="LACSCounts()" src="/img/oot/medal_5.png" :class="{ 'opacity-25': !getNumberItemsFromName('Spirit Medallion')  }" />
            <img title="Light Medaillon" v-if="medalsCounts()" src="/img/oot/medal_6.png" :class="{ 'opacity-25': !getNumberItemsFromName('Light Medallion')  }" />
            <img title="Greg the Green Rupee" v-if="gregCounts()" src="/img/oot/rupee.png" :class="{ 'opacity-25': !getNumberItemsFromName('Greg the Green Rupee')  }" />
            <img title="Ganon Boss Key" v-if="ganonBkSanity()" src="/img/oot/114_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ganon\'s Castle Boss Key')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Inventory</div>

            <img v-if="getNumberItemsFromName('Progressive Master Sword') > 3" title="Master Sword" src="/img/twilight_princess/23_3.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Master Sword') > 2" title="Master Sword" src="/img/twilight_princess/23_2.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Master Sword') > 1" title="Master Sword" src="/img/twilight_princess/23_1.png" />
            <img v-else title="Kokiri Sword" src="/img/twilight_princess/47_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Master Sword')  }" />
            <img v-if="getNumberItemsFromName('Hylian Shield')" src="/img/twilight_princess/26_1.png" title="Hylian Shield" />
            <img v-else src="/img/twilight_princess/25_1.png" title="Ordon Shield" :class="{ 'opacity-25': !getNumberItemsFromName('Ordon Shield')  }" />
            <img title="Iron Boots" src="/img/twilight_princess/32_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Iron Boots')  }" />
            <img v-if="getNumberItemsFromName('Strength Upgrade') > 2" title="Golden Gauntlets" src="/img/twilight_princess/21_3.png" />
            <img v-else-if="getNumberItemsFromName('Strength Upgrade') > 1" title="Silver Gauntlets" src="/img/twilight_princess/21_2.png" />
            <img v-else src="/img/oot/21_1.png" title="Goron Bracelet" :class="{ 'opacity-25': !getNumberItemsFromName('Strength Upgrade')  }" />
            <img src="/img/oot/30_1.png" title="Zora Armor" :class="{ 'opacity-25': !getNumberItemsFromName('Zora Armor')  }" />
            <img title="Shadow Crystal" :class="{ 'opacity-25': !getNumberItemsFromName('Shadow Crystal')  }" src="/img/twilight_princess/20_1.png" />

            <span class="mr-2"></span>


            <img v-if="getNumberItemsFromName('Horse Call') > 1" title="Ocarina of Time" src="/img/twilight_princess/46_1.png" />
            <img v-else src="/img/twilight_princess/35_1.png" title="Horse Call" :class="{ 'opacity-25': !getNumberItemsFromName('Horse Call')  }" />
            <img v-if="getNumberItemsFromName('Bomb Bag') > 2" title="Bomb Bag" src="/img/twilight_princess/5_3.png" />
            <img v-else-if="getNumberItemsFromName('Bomb Bag') > 1" title="Bomb Bag" src="/img/twilight_princess/5_2.png" />
            <img v-else-if="getNumberItemsFromName('Bomb Bag')" title="Bomb Bag" src="/img/twilight_princess/5_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Bomb Bag')  }" />
            <img title="Gale Boomerang" src="/img/twilight_princess/2_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Gale Boomerang')  }" />
            <img v-if="getNumberItemsFromName('Progressive Hero\'s Bow') > 2" title="Bow" src="/img/twilight_princess/6_3.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Hero\'s Bow') > 1" title="Bow" src="/img/twilight_princess/6_2.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Hero\'s Bow')" src="/img/twilight_princess/6_1.png" title="Bow" />
            <img v-else src="/img/twilight_princess/1_1.png" title="Slingshot" :class="{ 'opacity-25': !getNumberItemsFromName('Slingshot')  }" />
            <img src="/img/twilight_princess/9_1.png" title="Fire Arrow" :class="{ 'opacity-25': !getNumberItemsFromName('Bomb Arrow')  }" />
            <img v-if="getNumberItemsFromName('Progressive Clawshot') > 1" title="Double Clawshot" src="/img/oot/7_2.png" />
            <img v-else src="/img/twilight_princess/7_1.png" title="Clawshot" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Clawshot')  }" />
            <img title="Ball and Chain" src="/img/twilight_princess/8_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ball and Chain')  }" />
            <img title="Drehen" src="/img/twilight_princess/12_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Spinner')  }" />
            <img v-if="getNumberItemsFromName('Progressive Dominion Rod') > 1" title="Dominion Rod" src="/img/oot/11_1.png" />
            <img v-else title="Dominion Rod" src="/img/twilight_princess/10_1.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Dominion Rod')  }" />
            <img title="Bottle" src="/img/twilight_princess/3_1.png" :class="{ 'opacity-25': !hasBottle()  }" />
        </div>
    </div>
</template>
<script>
    /**
    * Twilight Princess
    *
    * By Default, Objectives are Dungeons rewards. But it can change depnding on the Bridge/Ganon Boss Key setting
    *
    * Bridge setting :
    *   0 - vanilla
    *   1 - always_open
    *   2 - stones
    *   3 - medallions
    *   4 - dungeon_rewards
    *   5 - dungeons
    *   6 - tokens
    *   7 - greg
    *
    *
    * Ganon Boss Key setting :
    *   0 - vanilla
    *   1 - anywhere
    *   2 - lacs_vanilla
    *   3 - lacs_stones
    *   4 - lacs_medallions
    *   5 - lacs_dungeon_rewards
    *   6 - lacs_dungeons
    *   7 - lacs_skull_tokens
    *
    *   If Triforce Hunt is on, Ganon Boss Key will always be behind the Triforce Pieces goal.
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

                var row_bridge = { title: 'Rainbow Bridge', value : null, details : null };
                if (this.data.slot_data.rainbow_bridge == 0) {
                    row_bridge.value = 'Vanilla';
                    row_bridge.details = 'Shadow & Spirit Medaillon';
                }
                else if (this.data.slot_data.rainbow_bridge == 1) {
                    row_bridge.value = 'Open';
                }
                else if (this.data.slot_data.rainbow_bridge == 2) {
                    row_bridge.value = 'Stones';
                    row_bridge.details = this.data.slot_data.rainbow_bridge_stones_required;
                }
                else if (this.data.slot_data.rainbow_bridge == 3) {
                    row_bridge.value = 'Medaillons';
                    row_bridge.details = this.data.slot_data.rainbow_bridge_medallions_required;
                }
                else if (this.data.slot_data.rainbow_bridge == 4) {
                    row_bridge.value = 'Rewards';
                    row_bridge.details = this.data.slot_data.rainbow_bridge_dungeon_rewards_required;
                }
                else if (this.data.slot_data.rainbow_bridge == 5) {
                    row_bridge.value = 'Dungeon completions';
                    row_bridge.details = this.data.slot_data.rainbow_bridge_dungeons_required;
                }
                else if (this.data.slot_data.rainbow_bridge == 6) {
                    row_bridge.value = 'Skultullas Tokens';
                    row_bridge.details = this.data.slot_data.rainbow_bridge_skull_tokens_required;
                }
                else if (this.data.slot_data.rainbow_bridge == 7) {
                    row_bridge.value = 'Greg';
                }

                res.push(row_bridge);

                var row_bk = { title: 'Ganon Castle Boss Key', value: null, details: null };
                if (this.data.slot_data.triforce_hunt) {
                    row_bk.value = 'Triforce Hunt';
                    row_bk.details = this.data.slot_data.triforce_hunt_pieces_required + ' out of ' + this.data.slot_data.triforce_hunt_pieces_total;
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 0) {
                    row_bk.value = 'Vanilla';
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 1) {
                    row_bk.value = 'Shuffled';
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 2) {
                    row_bk.value = 'LACS';
                    row_bk.details = 'Shadow & Spirit Medaillon';
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 3) {
                    row_bk.value = 'LACS Stones';
                    row_bk.details = this.data.slot_data.ganons_castle_boss_key_stones_required;
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 4) {
                    row_bk.value = 'LACS Medaillons';
                    row_bk.details = this.data.slot_data.ganons_castle_boss_key_medallions_required;
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 5) {
                    row_bk.value = 'LACS Rewards';
                    row_bk.details = this.data.slot_data.ganons_castle_boss_key_dungeon_rewards_required;
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 6) {
                    row_bk.value = 'LACS Dungeon completions';
                    row_bk.details = this.data.slot_data.ganons_castle_boss_key_dungeons_required;
                }
                else if (this.data.slot_data.ganons_castle_boss_key == 7) {
                    row_bk.value = 'LACS Skultullas Tokens';
                    row_bk.details = this.data.slot_data.ganons_castle_boss_key_skull_tokens_required;
                }

                res.push(row_bk);


                // Dungeon Rewards
                var row_tmp = { title: 'Dungeons Rewards are', value: 'Vanilla', details: null };
                if (this.data.slot_data.shuffle_dungeon_rewards == 1)
                    row_tmp.value = 'On their dungeons';
                else if (this.data.slot_data.shuffle_dungeon_rewards == 2)
                    row_tmp.value = 'Anywhere';

                res.push(row_tmp);

                var row_key = { title: 'Small Key configuration', value: null, details: null };
                var dlcs = [];
                if (this.data.slot_data.key_rings && this.data.slot_data.key_rings_count)
                    dlcs.push('Keyring (' + this.data.slot_data.key_rings_count + ')');
                if (this.data.slot_data.small_key_shuffle == 2)
                    dlcs.push('Shuffled on any dungeon');
                if (this.data.slot_data.small_key_shuffle == 3)
                    dlcs.push('Shuffled on overworld');
                if (this.data.slot_data.small_key_shuffle == 4)
                    dlcs.push('Shuffled anywhere');
                if (dlcs.length) {
                    row_key.value = dlcs.join(', ');
                    res.push(row_key);
                }

                var dlcs = [];
                if (this.data.slot_data.shuffle_master_sword)
                    dlcs.push('Master Sword');
                if (this.data.slot_data.shuffle_deku_nut_bag)
                    dlcs.push('Nuts');
                if (this.data.slot_data.shuffle_deku_stick_bag)
                    dlcs.push('Sticks');
                if (this.data.slot_data.shuffle_childs_wallet)
                    dlcs.push('Wallet');
                if (this.data.slot_data.shuffle_swim)
                    dlcs.push('Swim');
                if (this.data.slot_data.shuffle_fishing_pole)
                    dlcs.push('Fishing Pole');
                if (this.data.slot_data.shuffle_ocarina_buttons)
                    dlcs.push('Ocarina Buttons');


                var row_dlc = { title: 'Inventory Shuffle', value: null, details: null };
                if (dlcs.length) {
                    row_dlc.value = dlcs.join(', ');
                    res.push(row_dlc);
                }

                dlcs = [];
                if (this.data.slot_data.boss_key_shuffle == 2)
                    dlcs.push('Boss Keys (dungeon)');
                if (this.data.slot_data.boss_key_shuffle == 3)
                    dlcs.push('Boss Keys (OW)');
                if (this.data.slot_data.boss_key_shuffle == 4)
                    dlcs.push('Boss Keys');
                if (this.data.slot_data.shuffle_boss_souls)
                    dlcs.push('Boss Souls');
                if (this.data.slot_data.shuffle_shops && this.data.slot_data.shuffle_shops_item_amount)
                    dlcs.push('Shops (' + this.data.slot_data.shuffle_shops_item_amount + ')');
                if (this.data.slot_data.shuffle_skull_tokens == 1)
                    dlcs.push('Skultulla Tokens (Dungeons)');
                if (this.data.slot_data.shuffle_skull_tokens == 2)
                    dlcs.push('Skultulla Tokens (OW)');
                if (this.data.slot_data.shuffle_skull_tokens == 3)
                    dlcs.push('Skultulla Tokens');
                if (this.data.slot_data.shuffle_scrubs > 1)
                    dlcs.push('Scrubs');
                if (this.data.slot_data.shuffle_cows)
                    dlcs.push('Cows');
                if (this.data.slot_data.shuffle_pots == 1)
                    dlcs.push('Pots (Dungeons)');
                if (this.data.slot_data.shuffle_pots == 2)
                    dlcs.push('Pots (OW)');
                if (this.data.slot_data.shuffle_pots == 3)
                    dlcs.push('Pots');
                if (this.data.slot_data.shuffle_crates == 1)
                    dlcs.push('Crates (Dungeons)');
                if (this.data.slot_data.shuffle_crates == 2)
                    dlcs.push('Crates (OW)');
                if (this.data.slot_data.shuffle_crates == 3)
                    dlcs.push('Crates');
                if (this.data.slot_data.shuffle_freestanding_items == 1)
                    dlcs.push('Freestrandings (Dungeons)');
                if (this.data.slot_data.shuffle_freestanding_items == 2)
                    dlcs.push('Freestrandings (OW)');
                if (this.data.slot_data.shuffle_freestanding_items == 3)
                    dlcs.push('Freestrandings');
                if (this.data.slot_data.shuffle_beehives)
                    dlcs.push('Beehives');
                if (this.data.slot_data.shuffle_freestandings)
                    dlcs.push('Freestrandings');
                if (this.data.slot_data.shuffle_grass == 1)
                    dlcs.push('Grass (Dungeons)');
                if (this.data.slot_data.shuffle_grass == 2)
                    dlcs.push('Grass (OW)');
                if (this.data.slot_data.shuffle_grass == 3)
                    dlcs.push('Grass');
                if (this.data.slot_data.shuffle_trees)
                    dlcs.push('Trees');
                if (this.data.slot_data.shuffle_fish == 1)
                    dlcs.push('Fishes (Pond)');
                if (this.data.slot_data.shuffle_fish == 2)
                    dlcs.push('Fishes (OW)');
                if (this.data.slot_data.shuffle_fish == 3)
                    dlcs.push('Fishes');
                if (this.data.slot_data.shuffle_fountain_fairies)
                    dlcs.push('Fairies');
                if (this.data.slot_data.shuffle_stone_fairies)
                    dlcs.push('Stone Fairies');
                if (this.data.slot_data.shuffle_bean_fairies)
                    dlcs.push('Bean Fairies');
                if (this.data.slot_data.shuffle_song_fairies)
                    dlcs.push('Song Fairies');


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
            gerudoCard: function () {
                if (this.data.slot_data.hasOwnProperty('shuffle_gerudo_membership_card') && this.data.slot_data.shuffle_gerudo_membership_card) {
                    return true;
                }
                return 0;
            },
            triforceHunt: function () {
                if (this.data.slot_data.hasOwnProperty('triforce_hunt') && this.data.slot_data.triforce_hunt == 1) {
                    return this.data.slot_data.triforce_hunt_pieces_required;
                }
                return this.getNumberItemsFromName('Triforce Piece');
            },
            stonesCounts: function () {
                if (this.data.slot_data.hasOwnProperty('rainbow_bridge')) {
                    if ([2, 4, 5].includes(this.data.slot_data.rainbow_bridge) ||
                        !this.triforceHunt() && [3, 5, 6].includes(this.data.slot_data.ganons_castle_boss_key))
                        return true;
                    return false;
                }
                return true;
            },
            medalsCounts: function () {
                if (this.data.slot_data.hasOwnProperty('rainbow_bridge')) {
                    if ([3, 4, 5].includes(this.data.slot_data.rainbow_bridge) ||
                        !this.triforceHunt() && [4, 5, 6].includes(this.data.slot_data.ganons_castle_boss_key))
                        return true;
                    return false;
                }
                return true;
            },
            LACSCounts: function () {
                if (this.data.slot_data.hasOwnProperty('rainbow_bridge')) {
                    if ([0, 3, 4, 5].includes(this.data.slot_data.rainbow_bridge) ||
                        !this.triforceHunt() && [0, 2, 4, 5, 6].includes(this.data.slot_data.ganons_castle_boss_key))
                        return true;
                    return false;
                }
                return true;
            },
            gregCounts: function () {
                if (this.data.slot_data.hasOwnProperty('rainbow_bridge') &&
                    (this.data.slot_data.rainbow_bridge == 7 || this.data.slot_data.rainbow_bridge_greg_modifier) ||
                    !this.triforceHunt() && [3, 4, 5, 7].includes(this.data.slot_data.ganons_castle_boss_key) && this.data.slot_data.ganons_castle_boss_key_greg_modifier) {
                    return true;
                }
                return false;
            },
            ganonBkSanity: function () {
                if (this.data.slot_data.hasOwnProperty('ganons_castle_boss_key') &&
                    (this.data.slot_data.ganons_castle_boss_key == 1)) {
                    return true;
                }
                return false;
            },
            skullsTokensCounts: function () {
                if (this.data.slot_data.hasOwnProperty('rainbow_bridge') &&
                    (this.data.slot_data.rainbow_bridge == 6 ||
                    !this.triforceHunt() && this.data.slot_data.ganons_castle_boss_key == 7)) {
                    return this.data.slot_data.rainbow_bridge_skull_tokens_required;
                }
                return 0;
            },
            getNumberItemsNameStart: function (name) {
                var res = 0;
                if (this.gamedata && this.gamedata.item_name_to_id) {
                    var bottle_array = [];
                    for (var key in this.gamedata.item_name_to_id) {
                        if (key.startsWith(name)) {
                            bottle_array.push(this.gamedata.item_name_to_id[key]);
                        }
                    }
                    for (var x = 0; x < this.data.tracker_data.player_items_received.length; x++) {
                        if (bottle_array.includes(this.data.tracker_data.player_items_received[x][0]))
                            res++;
                    }
                }
                return res;
            }, 
            hasDekuSticks: function () {
                if (this.data.slot_data.hasOwnProperty('shuffle_deku_stick_bag') && this.data.slot_data.shuffle_deku_stick_bag) {
                    return this.getNumberItemsFromName('Progressive Stick Capacity');
                }
                return 1;
            },
            shuffleKnife: function () {
                if (this.data.slot_data.hasOwnProperty('shuffle_merchants') && this.data.slot_data.shuffle_merchants > 1) {
                    return 1;
                }
                return 0;
            },
            shuffleSwim: function () {
                if (this.data.slot_data.hasOwnProperty('shuffle_swim')) {
                    return this.data.slot_data.shuffle_swim;
                }
                return 0;
            },
            hasMasterSword: function () {
                if (this.data.slot_data.hasOwnProperty('shuffle_master_sword') && this.data.slot_data.shuffle_master_sword == 1) {
                    return this.getNumberItemsFromName('Master Sword');
                }
                return 1;
            },
            hasBottle: function () {
                if (this.getNumberItemsFromName('Empty Bottle') || this.getNumberItemsNameStart('Bottle with')) {
                    return true;
                }
                return false;
            }
        },
  components: {
  },
};
</script>
