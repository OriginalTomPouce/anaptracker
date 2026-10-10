<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="getGoalStars()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Power Star')  }"><img title="Power Star" src="/img/sm64/star.png" />x{{ getNumberItemsFromName('Power Star') }} </span> / {{ getGoalStars() }}</span>
            <span v-else class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Power Star')  }"><img title="Power Star" src="/img/sm64/star.png" />x{{ getNumberItemsFromName('Power Star') }} </span>

            <img title="Basement Key" src="/img/sm64/keys/key_basement.png" :class="{ 'opacity-25': !basementKey()  }" />
            <img title="Upstairs Key" src="/img/sm64/keys/key_upstairs.png" :class="{ 'opacity-25': !upstairsKey()  }" />
            <!--
    <img v-if="getNumberItemsFromName('Progressive Key') > 1" src="/img/sm64/keys/key_both.png" class="inline-block mr-1 w-[16px] h-[16px]" />
    <img v-else-if="getNumberItemsFromName('Progressive Key') > 0" src="/img/sm64/keys/key_basement.png" class="inline-block mr-1 w-[16px] h-[16px]" />
    <img v-else-if="getNumberItemsFromName('Upstairs Key') && getNumberItemsFromName('Basement Key')" src="/img/sm64/keys/key_both.png" class="inline-block mr-1 w-[16px] h-[16px]" />
    <img v-else-if="getNumberItemsFromName('Upstairs Key')" src="/img/sm64/keys/key_upstairs.png" class="inline-block mr-1 w-[16px] h-[16px]" />
    <img v-else-if="getNumberItemsFromName('Basement Key')" src="/img/sm64/keys/key_basement.png" class="inline-block mr-1 w-[16px] h-[16px]" />
    <img v-else src="/img/sm64/keys/key.png" class="inline-block mr-1 w-[16px] h-[16px] opacity-25" />
    -->
        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Abilities</div>

            <span v-if="paintingRando()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getUnlockedPaintings()  }"><img title="Paintings" src="/img/sm64/painting.png" />x{{ getUnlockedPaintings() }} </span></span>

            <img title="Wing Cap" src="/img/sm64/blocks/block_red.png" :class="{ 'opacity-25': !getNumberItemsFromName('Wing Cap')  }" />
            <img title="Vanish Cap" src="/img/sm64/blocks/block_blue.png" :class="{ 'opacity-25': !getNumberItemsFromName('Vanish Cap')  }" />
            <img title="Metal Cap" src="/img/sm64/blocks/block_green.png" :class="{ 'opacity-25': !getNumberItemsFromName('Metal Cap')  }" />

            <span v-if="moveShuffled()" class="mr-2"></span>
            <img v-if="moveShuffled()" title="Climb" src="/img/sm64/moves/climb.png" :class="{ 'opacity-25': !getNumberItemsFromName('Climb')  }" />
            <img v-if="moveShuffled()" title="Ledge Grab" src="/img/sm64/moves/ledge_grab.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ledge Grab')  }" />
            <img v-if="moveShuffled()" title="Ground Pound" src="/img/sm64/moves/ground_pound.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ground Pound')  }" />
            <img v-if="moveShuffled()" title="Triple Jump" src="/img/sm64/moves/triple_jump.png" :class="{ 'opacity-25': !getNumberItemsFromName('Triple Jump')  }" />
            <img v-if="moveShuffled()" title="Long Jump" src="/img/sm64/moves/long_jump.png" :class="{ 'opacity-25': !getNumberItemsFromName('Long Jump')  }" />
            <img v-if="moveShuffled()" title="Wall Kick" src="/img/sm64/moves/wall_jump.png" :class="{ 'opacity-25': !getNumberItemsFromName('Wall Kick')  }" />
            <img v-if="moveShuffled()" title="Side Flip" src="/img/sm64/moves/sideflip.png" :class="{ 'opacity-25': !getNumberItemsFromName('Side Flip')  }" />
            <img v-if="moveShuffled()" title="Backflip" src="/img/sm64/moves/backflip.png" :class="{ 'opacity-25': !getNumberItemsFromName('Backflip')  }" />
            <img v-if="moveShuffled()" title="Kick" src="/img/sm64/moves/kick.png" :class="{ 'opacity-25': !getNumberItemsFromName('Kick')  }" />
            <img v-if="moveShuffled()" title="Dive" src="/img/sm64/moves/dive.png" :class="{ 'opacity-25': !getNumberItemsFromName('Dive')  }" />
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
  name: "gDataMario64",
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
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            getGoalStars: function () {
                if (this.data.slot_data.StarsToFinish) {
                    return this.data.slot_data.StarsToFinish;
                }
                return 0;
            },
            upstairsKey: function () {
                if (this.getNumberItemsFromName('Second Floor Key') || this.getNumberItemsFromName('Progressive Key') > 1)
                    return true;
                return false;
                
            },
            basementKey: function () {
                if (this.getNumberItemsFromName('Basement Key') || this.getNumberItemsFromName('Progressive Key'))
                    return true;
                return false;
            },
            moveShuffled: function () {
                if (this.data.slot_data.hasOwnProperty('MoveRandoVec')) {
                    return this.data.slot_data.MoveRandoVec;
                }
                return 1;
            },
            paintingRando: function () {
                if (this.data.slot_data.hasOwnProperty('PaintingRando')) {
                    return this.data.slot_data.PaintingRando;
                }
                return this.getUnlockedPaintings();
            },
            getUnlockedPaintings: function() {
                return this.$parent.getNumberItemsFromGroup(["Painting Unlock CCM", "Painting Unlock DDD", "Painting Unlock LLL", "Painting Unlock SL", "Painting Unlock SSL", "Painting Unlock THI", "Painting Unlock TTC", "Painting Unlock TTM", "Painting Unlock WDW", "Painting Unlock WF"]);
            },
        },
  components: {
  },
};
</script>
