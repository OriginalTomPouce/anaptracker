<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="emblemsRequired()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Lucky Emblem')  }"><img title="Lucky Emblem" src="/img/kingdom_hearts_2/Lucky Emblem.png" />x{{ getNumberItemsFromName('Lucky Emblem') }} </span> / {{ emblemsRequired() }}</span>
            <span v-else class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Lucky Emblem')  }"><img title="Lucky Emblem" src="/img/kingdom_hearts_2/Lucky Emblem.png" />x{{ getNumberItemsFromName('Lucky Emblem') }} </span>
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Abilities</div>

            <span class="mr-2 text-xs" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Fire')  }"><img title="Fire Element" src="/img/kingdom_hearts_2/Fire.png" />x{{getNumberItemsFromName('Progressive Fire')}}</span>
            <span class="mr-2 text-xs" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Blizzard')  }"><img title="Blizzard Element" src="/img/kingdom_hearts_2/Blizzard.png" />x{{getNumberItemsFromName('Progressive Blizzard')}}</span>
            <span class="mr-2 text-xs" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Thunder')  }"><img title="Thunder Element" src="/img/kingdom_hearts_2/Thunder.png" />x{{getNumberItemsFromName('Progressive Thunder')}}</span>
            <span class="mr-2 text-xs" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Cure')  }"><img title="Cure Element" src="/img/kingdom_hearts_2/Cure.png" />x{{getNumberItemsFromName('Progressive Cure')}}</span>
            <span class="mr-2 text-xs" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Gravity')  }"><img title="Gravity Element" src="/img/kingdom_hearts_2/Magnet.png" />x{{getNumberItemsFromName('Progressive Gravity')}}</span>
            <span class="mr-2 text-xs" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Aero')  }"><img title="Aero Element" src="/img/kingdom_hearts_2/Reflect.png" />x{{getNumberItemsFromName('Progressive Aero')}}</span>

        </div>
    </div>
</template>
<script>
    /**
    * Kingdom Hearts
    *
    * Goal is mainly determined by the Lucky Emblems required to get through the final boss.
    */
    export default {
        name: "gDataKingdomHearts",
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
                return [];
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            emblemsRequired: function () {
                if (this.data.slot_data.hasOwnProperty('required_lucky_emblems_door')) {
                    if (this.data.slot_data.required_lucky_emblems_door > this.data.slot_data.required_lucky_emblems_eotw)
                        return this.data.slot_data.required_lucky_emblems_door;
                    return this.data.slot_data.required_lucky_emblems_eotw;
                }
                return 0;
            }
        },
        components: {
        },
    };
</script>
