<template>
    <div class="inline-block">
        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>
            <img title="Diamond Star" src="/img/pm_ttyd/DiamondStar.png" :class="{ 'opacity-25': !getNumberItemsFromName('Diamond Star')  }" />
            <img title="Emerald Star" src="/img/pm_ttyd/EmeraldStar.png" :class="{ 'opacity-25': !getNumberItemsFromName('Emerald Star')  }" />
            <img title="Gold Star" src="/img/pm_ttyd/GoldStar.png" :class="{ 'opacity-25': !getNumberItemsFromName('Gold Star')  }" />
            <img title="Ruby Star" src="/img/pm_ttyd/RubyStar.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ruby Star')  }" />
            <img title="Sapphire Star" src="/img/pm_ttyd/SapphireStar.png" :class="{ 'opacity-25': !getNumberItemsFromName('Sapphire Star')  }" />
            <img title="Garnet Star"  src="/img/pm_ttyd/GarnetStar.png" :class="{ 'opacity-25': !getNumberItemsFromName('Garnet Star')  }" />
            <img title="Crystal Star" src="/img/pm_ttyd/CrystalStar.png" :class="{ 'opacity-25': !getNumberItemsFromName('Crystal Star')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Inventory</div>

            <img v-if="getNumberItemsFromName('Progressive Hammer') > 1" title="Ultra Hammer" src="/img/pm_ttyd/UltraHammer.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Hammer')" title="Super Hammer" src="/img/pm_ttyd/SuperHammer.png" />
            <img v-else src="/img/pm_ttyd/Hammer.png" title="Hammer" />

            <img v-if="getNumberItemsFromName('Progressive Boots') > 1" title="Ultra Boots" src="/img/pm_ttyd/UltraBoots.png" />
            <img v-else-if="getNumberItemsFromName('Progressive Boots')" title="Super Boots" src="/img/pm_ttyd/SuperBoots.png" />
            <img v-else src="/img/pm_ttyd/Boots.png" title="Boots" />

            <img title="Plane Mode" src="/img/pm_ttyd/Plane.png" :class="{ 'opacity-25': !getNumberItemsFromName('Plane Mode')  }" />
            <img title="Paper Mode" src="/img/pm_ttyd/Paper.png" :class="{ 'opacity-25': !getNumberItemsFromName('Paper Mode')  }" />
            <img title="Tube Mode" src="/img/pm_ttyd/Tube.png" :class="{ 'opacity-25': !getNumberItemsFromName('Tube Mode')  }" />
            <img title="Boat Mode" src="/img/pm_ttyd/Boat.png" :class="{ 'opacity-25': !getNumberItemsFromName('Boat Mode')  }" />
            <span class="mr-2"></span>

            <img title="Blimp Ticket" src="/img/pm_ttyd/BlimpTicket.png" :class="{ 'opacity-25': !getNumberItemsFromName('Blimp Ticket')  }" />
            <img title="Old Letter" src="/img/pm_ttyd/OldLetter.png" :class="{ 'opacity-25': !getNumberItemsFromName('Old Letter')  }" />
            <img title="Train Ticket" src="/img/pm_ttyd/TrainTicket.png" :class="{ 'opacity-25': !getNumberItemsFromName('Train Ticket')  }" />

        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Partners</div>

            <img title="Goombella" src="/img/pm_ttyd/Goombella.png" :class="{ 'opacity-25': !getNumberItemsFromName('Goombella')  }" />
            <img title="Koops" src="/img/pm_ttyd/Koops.png" :class="{ 'opacity-25': !getNumberItemsFromName('Koops')  }" />
            <img title="Flurrie" src="/img/pm_ttyd/Flurrie.png" :class="{ 'opacity-25': !getNumberItemsFromName('Flurrie')  }" />
            <img title="Yoshi" :src="yoshi()" :class="{ 'opacity-25': !getNumberItemsFromName('Yoshi')  }" />
            <img title="Vivian" src="/img/pm_ttyd/Vivian.png" :class="{ 'opacity-25': !getNumberItemsFromName('Vivian')  }" />
            <img title="Bobbery" src="/img/pm_ttyd/Bobbery.png" :class="{ 'opacity-25': !getNumberItemsFromName('Bobbery')  }" />
            <img title="Ms. Mowz" src="/img/pm_ttyd/Mowz.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ms. Mowz')  }" />
        </div>
    </div>
</template>
<script>
    /**
    * Paper Mario : The Thousand Year Door
    *
    * Goal are
    *   1 - Shadow Queen (beat the final boss with a set number of star pieces to get)
    *   2 - Collect Star Pieces (collect a set number of star pieces)
    *   3 - Beat Bonetail
    *
    */
    export default {
        name: "gDataPaperMarioTTYD",
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
                if (!this.data.slot_data.hasOwnProperty('goal'))
                    return [];
                var res = [];

                var row_goal = { title: 'Goal', value: 'Shadow Queen', details: null };
                var row_stars = { title: 'Stars required to goal', value: this.data.slot_data.goal_stars, details: null };
                if (this.data.slot_data.goal == 1) {
                    row_goal.value = 'Shadow Queen';
                }
                else if (this.data.slot_data.goal == 2) {
                    row_goal.value = 'Collect Star Pieces';
                }
                else if (this.data.slot_data.goal == 3) {
                    row_goal.value = 'Bonetail';
                }

                res.push(row_goal);
                if (this.data.slot_data.goal < 3) {
                    res.push(row_stars);
                    row_stars = { title: 'Stars to enter Shadow Palace', value: this.data.slot_data.palace_stars, details: null };
                    res.push(row_stars);

                }


                var row_skip = { title: 'Palace skip', value: 'Off', details: null };
                if (this.data.slot_data.palace_skip) {
                    row_skip.value = 'On';

                }
                res.push(row_skip);


                // Star Shuffle
                var row_tmp = { title: 'Stars are', value: 'Vanilla', details: null };
                if (this.data.slot_data.star_shuffle == 2)
                    row_tmp.value = 'On Star pool';
                else if (this.data.slot_data.star_shuffle == 3)
                    row_tmp.value = 'Anywhere';

                res.push(row_tmp);


                var dlcs = [];
                if (this.data.slot_data.piecesanity == 2)
                    dlcs.push('Star Pieces');
                if (this.data.slot_data.shinesanity == 2)
                    dlcs.push('Shine Sprites');

                var row_dlc = { title: 'Extra Shuffle', value: null, details: null };
                if (dlcs.length) {
                    row_dlc.value = dlcs.join(', ');
                    res.push(row_dlc);
                }

                return res;
            },
            yoshi: function () {
                if (this.data.slot_data.hasOwnProperty('yoshi_color')) {
                    if (this.data.slot_data.yoshi_color == 1)
                        return '/img/pm_ttyd/RYoshi.png';
                    if (this.data.slot_data.yoshi_color == 2)
                        return '/img/pm_ttyd/BYoshi.png';
                    if (this.data.slot_data.yoshi_color == 3)
                        return '/img/pm_ttyd/OYoshi.png';
                    if (this.data.slot_data.yoshi_color == 4)
                        return '/img/pm_ttyd/PYoshi.png';
                    if (this.data.slot_data.yoshi_color == 5)
                        return '/img/pm_ttyd/DYoshi.png';
                    if (this.data.slot_data.yoshi_color == 6)
                        return '/img/pm_ttyd/WYoshi.png';
                }
                return '/img/pm_ttyd/GYoshi.png';
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
        },
        components: {
        },
    };
</script>
