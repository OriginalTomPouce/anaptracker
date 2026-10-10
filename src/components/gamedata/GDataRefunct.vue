<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="getGoalGrass()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromCategory('Grasses')  }"><img title="Grass" src="/img/refunct/grass.png" />x{{ getNumberItemsFromCategory('Grasses') }} </span> / {{ getGoalGrass() }}</span>
            <span v-else class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getNumberItemsFromCategory('Grasses')  }"><img title="Grass" src="/img/refunct/grass.png" />x{{ getNumberItemsFromCategory('Grasses') }} </span>

            <span v-if="getClusterGoal()"  class="mr-2 font-bold text-xs font-bold" title="Cluster Goal" :class="{ 'opacity-25': !hasClusterGoal()  }" ><img title="Paintings" src="/img/refunct/cluster_goal.png" />{{ getClusterGoal() }}</span>
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Abilities</div>

            <span class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getUnlockedClusters()  }"><img title="Paintings" src="/img/refunct/cluster.png" />x{{ getUnlockedClusters() }} </span></span>

            <span v-if="getAvailableMinigames()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromCategory('Minigames')  }"><img title="Minigames" src="/img/refunct/cluster_game.png" />x{{ getNumberItemsFromCategory('Minigames') }} </span> / {{ getAvailableMinigames() }}</span>
            <span v-else class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getNumberItemsFromCategory('Minigames')  }"><img title="Minigames" src="/img/refunct/cluster_game.png" />x{{ getNumberItemsFromCategory('Minigames') }} </span>

            <span class="mr-2"></span>
            <img title="Ledge Grap" src="/img/refunct/moves/ledge_grab.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ledge Grab')  }" />
            <img title="Swim" src="/img/refunct/moves/swim.png" :class="{ 'opacity-25': !getNumberItemsFromName('Swim')  }" />
            <img v-if="getNumberItemsFromName('Progressive Wall Jump') > 1" title="Continuous Wall Jump" src="/img/refunct/moves/wall_jump_2.png" />
            <img v-else title="Wall Jump" src="/img/refunct/moves/wall_jump_2.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Wall Jump')  }" />

            <span class="mr-2"></span>
            <img title="Green Cubes Bag" src="/img/refunct/blocks/block_green.png" :class="{ 'opacity-25': !getNumberItemsFromName('Green Cubes Bag')  }" />
            <img title="Red Cubes Bag" src="/img/refunct/blocks/block_red.png" :class="{ 'opacity-25': !getNumberItemsFromName('Red Cubes Bag')  }" />
            <img title="Lifts" src="/img/refunct/blocks/lift.png" :class="{ 'opacity-25': !getNumberItemsFromName('Lifts')  }" />
            <img title="Pipes" src="/img/refunct/blocks/pipe.png" :class="{ 'opacity-25': !getNumberItemsFromName('Pipes')  }" />
        </div>
    </div>
</template>
    
<script>

/**
* Super Mario 64
* 
* Goal is mainly determined by the Power Stars required to get through the infinite stairs.
* You also need at least the Upper Key (depending on Key settings).
* 
* By default, we always consider that move shuffle is on.
*/ 
export default {
  name: "gDataRefunct",
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

                if (this.data.slot_data.StarsToFinish > 0) {
                    res.push({ title: 'Stars for endless stairs', value: this.data.slot_data.StarsToFinish, details: null });
                }
                if (this.data.slot_data.FirstBowserDoorCost > 0) {
                    res.push({ title: 'Stars for lobby\'s door', value: this.data.slot_data.FirstBowserDoorCost, details: null });
                }
                if (this.data.slot_data.BasementDoorCost > 0) {
                    res.push({ title: 'Stars for basement door', value: this.data.slot_data.BasementDoorCost, details: null });
                }
                if (this.data.slot_data.SecondFloorDoorCost > 0) {
                    res.push({ title: 'Stars for 3F door', value: this.data.slot_data.SecondFloorDoorCost, details: null });
                }


                return res;
            },
            getClusterGoal: function () {
                if (this.data.slot_data.hasOwnProperty('goal_c'))
                    return this.data.slot_data.goal_c;
                return 0;
            },
            hasClusterGoal: function () {
                if (this.data.slot_data.hasOwnProperty('goal_c') && this.getNumberItemsFromName('Cluster ' + this.data.slot_data.goal_c.toString()))
                    return true;
                return false;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            getNumberItemsFromCategory: function(group) {
                return this.$parent.getNumberItemsFromCategory(group);
            },
            getAvailableMinigames: function() {
                if (this.data.slot_data.hasOwnProperty('minigames')) {
                    return this.data.slot_data.minigames.length;
                }
                return 0;
            },
            getGoalGrass: function () {
                if (this.data.slot_data.hasOwnProperty('required_grass')) {
                    return this.data.slot_data.required_grass;
                }
                return 0;
            },
            getUnlockedClusters: function () {
                return this.getNumberItemsFromCategory('Clusters')
            },
        },
  components: {
  },
};
</script>
