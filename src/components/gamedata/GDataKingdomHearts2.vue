<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="emblemHunt() && getGoalEmblems()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Lucky Emblem')  }"><img title="Lucky Emblem" src="/img/kingdom_hearts_2/Lucky Emblem.png" />x{{ getNumberItemsFromName('Lucky Emblem') }} </span> / {{ getGoalEmblems() }}</span>
            <span v-else-if="emblemHunt()" class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Lucky Emblem')  }"><img title="Lucky Emblem" src="/img/kingdom_hearts_2/Lucky Emblem.png" />x{{ getNumberItemsFromName('Lucky Emblem') }} </span>

            <span v-if="bountyHunt() && getGoalBounty()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Bounty')  }"><img title="Bounty" src="/img/kingdom_hearts_2/Bounty.png" />x{{ getNumberItemsFromName('Bounty') }} </span> / {{ bountyHunt() }}</span>
            <span v-else-if="bountyHunt() || getNumberItemsFromName('Bounty')" class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Bounty')  }"><img title="Bounty" src="/img/kingdom_hearts_2/Bounty.png" />x{{ getNumberItemsFromName('Bounty') }} </span>

            <img v-if="proofHunt()" title="Proof of Connection" src="/img/kingdom_hearts_2/Proof of Connection.png" :class="{ 'opacity-25': !getNumberItemsFromName('Proof of Connection')  }" />
            <img v-if="proofHunt()" title="Proof of Nonexistence" src="/img/kingdom_hearts_2/Proof of Nonexistence.png" :class="{ 'opacity-25': !getNumberItemsFromName('Proof of Nonexistence')  }" />
            <img v-if="proofHunt()" title="Proof of Peace" src="/img/kingdom_hearts_2/Proof of Tranquility.png" :class="{ 'opacity-25': !getNumberItemsFromName('Proof of Peace')  }" />
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Abilities</div>

            <img title="Fire Element" src="/img/kingdom_hearts_2/Fire.png" :class="{ 'opacity-25': !getNumberItemsFromName('Fire Element')  }" />
            <img title="Blizzard Element" src="/img/kingdom_hearts_2/Blizzard.png" :class="{ 'opacity-25': !getNumberItemsFromName('Blizzard Element')  }" />
            <img title="Thunder Element" src="/img/kingdom_hearts_2/Thunder.png" :class="{ 'opacity-25': !getNumberItemsFromName('Thunder Element')  }" />
            <img title="Cure Element" src="/img/kingdom_hearts_2/Cure.png" :class="{ 'opacity-25': !getNumberItemsFromName('Cure Element')  }" />
            <img title="Magnet Element" src="/img/kingdom_hearts_2/Magnet.png" :class="{ 'opacity-25': !getNumberItemsFromName('Magnet Element')  }" />
            <img title="Reflect Element" src="/img/kingdom_hearts_2/Reflect.png" :class="{ 'opacity-25': !getNumberItemsFromName('Reflect Element')  }" />
            <span class="mr-2"></span>
            <img title="Valor Form" src="/img/kingdom_hearts_2/Valor Orb.png" :class="{ 'opacity-25': !getNumberItemsFromName('Valor Form')  }" />
            <img title="Wisdom Form" src="/img/kingdom_hearts_2/Wisdom Orb.png" :class="{ 'opacity-25': !getNumberItemsFromName('Wisdom Form')  }" />
            <img title="Limit Form" src="/img/kingdom_hearts_2/Limit Orb.png" :class="{ 'opacity-25': !getNumberItemsFromName('Limit Form')  }" />
            <img title="Master Form" src="/img/kingdom_hearts_2/Master Orb.png" :class="{ 'opacity-25': !getNumberItemsFromName('Master Form')  }" />
            <img title="Final Form" src="/img/kingdom_hearts_2/Final Orb.png" :class="{ 'opacity-25': !getNumberItemsFromName('Final Form')  }" />
        </div>
    </div>
</template>
    
<script>

/**
* Kingdom Hearts 2
* 
* Goal options are :
* 0 - Three Proofs
* 1 - Lucky Emblem Hunt
* 2 - Bounty
* 3 - Bounty & Lucky Emblems
*/ 
export default {
        name: "gDataKingdomHearts2",
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
            proofHunt: function () {
                if (this.data.slot_data.hasOwnProperty('Goal')) {
                    if (this.data.slot_data.Goal == 0) 
                        return 1;
                    return 0;
                }
                return 1;
            },
            bountyHunt: function () {
                if (this.data.slot_data.hasOwnProperty('Goal')) {
                    if ([2, 3].includes(this.data.slot_data.Goal))
                        return this.data.slot_data.BountyRequired;
                    return 0;
                }
                return 1;
            },
            emblemHunt: function () {
                if (this.data.slot_data.hasOwnProperty('Goal')) {
                    if ([1, 3].includes(this.data.slot_data.Goal))
                        return this.data.slot_data.LuckyEmblemsRequired;
                    return 0;
                }
                return 1;
            },
            getGoalEmblems: function () {
                if (this.data.slot_data.hasOwnProperty('LuckyEmblemsRequired')) {
                    return this.data.slot_data.LuckyEmblemsRequired;
                }
                return 0;
            },
            getGoalBounty: function () {
                if (this.data.slot_data.hasOwnProperty('BountyRequired')) {
                    return this.data.slot_data.BountyRequired;
                }
                return 0;
            }
        },
  components: {
  },
};
</script>
