<template>
    <div class="inline-block">

        <div v-if="getGoalEggs() || !slotData()" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="getGoalEggs()" class="mr-1 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Golden Yoshi Egg')  }"><img src="/img/smw/items/yoshi_egg.png" title="Yoshi Egg" />x{{ getNumberItemsFromName('Golden Yoshi Egg') }} </span> / {{ getGoalEggs() }}</span>
            <span v-else-if="!slotData()" class="mr-1 text-xs font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Golden Yoshi Egg')  }"><img src="/img/smw/items/yoshi_egg.png" title="Yoshi Egg" />x{{ getNumberItemsFromName('Golden Yoshi Egg') }} </span>

        </div>

        <div v-if="moveShuffled()" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Moves</div>

            <img title="Yellow Switch" src="/img/smw/items/ysp_full.png" :class="{ 'opacity-25': !getNumberItemsFromName('Yellow Switch Palace')  }" />
            <img title="Green Switch" src="/img/smw/items/gsp_full.png" :class="{ 'opacity-25': !getNumberItemsFromName('Green Switch Palace')  }" />
            <img title="Red Switch" src="/img/smw/items/rsp_full.png" :class="{ 'opacity-25': !getNumberItemsFromName('Red Switch Palace')  }" />
            <img title="Blue Switch" src="/img/smw/items/bsp_full.png" :class="{ 'opacity-25': !getNumberItemsFromName('Blue Switch Palace')  }" />
            <span class="mr-2"></span>
            <img v-if="getNumberItemsFromName('Progressive Run') > 1" title="Run (on walls !)" src="/img/smw/items/run2.png" />
            <img v-else title="Run" src="/img/smw/items/run.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Run')  }" />
            <img title="Carry" src="/img/smw/items/carry.png" :class="{ 'opacity-25': !getNumberItemsFromName('Carry')  }" />
            <img title="Climb" src="/img/smw/items/climb.png" :class="{ 'opacity-25': !getNumberItemsFromName('Climb')  }" />
            <img v-if="getNumberItemsFromName('Progressive Swim') > 1" title="Swim (underwater)" src="/img/smw/items/swim2.png" />
            <img v-else title="Swim (surface)" src="/img/smw/items/swim.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Swim')  }" />
            <img title="Spin Jump" src="/img/smw/items/spin_jump.png" :class="{ 'opacity-25': !getNumberItemsFromName('Spin Jump')  }" />
            <img title="Powerup - Mushroom" src="/img/smw/items/big_mario.png" :class="{ 'opacity-25': !getNumberItemsFromName('Progressive Powerup')  }" />
            <img title="Powerup - Fire Flower" src="/img/smw/items/fire_mario.png" :class="{ 'opacity-25': getNumberItemsFromName('Progressive Powerup') < 2  }" />
            <img title="Powerup - Cape" src="/img/smw/items/cape_mario.png" :class="{ 'opacity-25': getNumberItemsFromName('Progressive Powerup') < 3 }" />
            <span class="mr-2"></span>
            <img title="P-Switch" src="/img/smw/items/p_switch.png" :class="{ 'opacity-25': !getNumberItemsFromName('P-Switch')  }" />
            <img title="P-Balloon" src="/img/smw/items/p_balloon.png" :class="{ 'opacity-25': !getNumberItemsFromName('P-Balloon')  }" />
        </div>
    </div>
</template>
    
<script>


    /**
    * Super Mario World
    *
    * Goal is to beat Bowser of get Yoshi's Eggs.
    * 
    */
export default {
  name: "gDataSuperMarioWorld",
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
            slotData: function () {
                // TODO : placeholder value because Eggs' requirements are not displayed the slot data.
                return this.data.slot_data.hasOwnProperty('blocksanity');
            },
            getGoalEggs: function () {
                // TODO : placeholder value because Eggs' requirements are not displayed the slot data.
                if (this.data.slot_data.hasOwnProperty('goal') && this.data.slot_data.goal == 2) {
                    return this.data.slot_data.required_egg_count;
                }
                return 0;
            },
            moveShuffled: function () {
                if (this.data.slot_data.MoveRandoVec) {
                    return this.data.slot_data.MoveRandoVec;
                }
                return 1;
            }
        },
  components: {
  },
};
</script>
