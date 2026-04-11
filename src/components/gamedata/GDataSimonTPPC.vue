<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="getGoalPuules()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getPuules()  }">🧩 x{{ getPuules() }} </span> / {{ getGoalPuules() }}</span>
            <span v-else class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getPuules()  }">🧩 x{{ getPuules() }} </span>

        </div>
    </div>
</template>
    
<script>

/**
* Pokepelago
* 
* Count puzzle pieces and win.
*/ 
export default {
        name: "gDataSimonTPPC",
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

                return res;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            getGoalPuules: function () {
                if (this.data.slot_data.solve_target) {
                    return this.data.slot_data.solve_target;
                }
                return 0;
            },
            getPuules: function () {
                return this.$parent.getNumberItemsFromCategory('Puzzle');
            },
        },
  components: {
  },
};
</script>
