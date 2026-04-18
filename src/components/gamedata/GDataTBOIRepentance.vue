<template>

    <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
        <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Chapters</div>

        <img title="The Womb" src="/img/tboi/Womb.png" :class="{ 'opacity-35': !getNumberItemsFromGroup(['Womb Unlock', 'Utero Unlock', 'Scared Womb Unlock'])  }" />
        <img title="Blue Womb" src="/img/tboi/Blue_Womb.png" :class="{ 'opacity-35': !getNumberItemsFromName('??? Unlock')  }" />
        <span class="mr-2"></span>
        <img title="Cathedral" src="/img/tboi/Cathedral.png" :class="{ 'opacity-35': !getNumberItemsFromName('Cathedral Unlock')  }" />
        <img title="The Chest" src="/img/tboi/Chest.png" :class="{ 'opacity-35': !getNumberItemsFromName('The Polaroid Unlock')  }" />
        <span class="mr-2"></span>
        <img title="Sheol" src="/img/tboi/Sheol.png" :class="{ 'opacity-35': !getNumberItemsFromName('Sheol Unlock')  }" />
        <img title="Dark Room" src="/img/tboi/Dark_Room.png" :class="{ 'opacity-35': !getNumberItemsFromName('The Negative Unlock')  }" />
        <span class="mr-2"></span>
        <img title="Mega Satan" src="/img/tboi/Mega_Satan.png" :class="{ 'opacity-35': !getNumberItemsFromName('Key Pieces Unlock')  }" />
        <span class="mr-2"></span>
        <img title="The Void" src="/img/tboi/The_Void.png" :class="{ 'opacity-35': !getNumberItemsFromName('Undefined Unlock')  }" />
    </div>
</template>
    
<script>

    /**
    * The Binding of Isaac : Repentance
    *
    * To complete the game, you have to beat a list of goals (beat bosses).
    *
    */
    export default {
        name: "gDataTBOIRepentance",
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
                var row_goal = { title: 'Goals', value: '', details: null };
                row_goal.value = this.data.slot_data.options.goals.join(', ');

                res.push(row_goal);


                var row_exclude = { title: 'Excluded', value: '', details: null };
                row_exclude.value = this.data.slot_data.options.excluded_areas.join(', ');

                if (row_exclude.value != '') {
                    res.push(row_exclude);
                }

                return res;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            getNumberItemsFromGroup: function (name) {
                return this.$parent.getNumberItemsFromGroup(name);
            },
        },
        components: {
        },
    };
</script>
