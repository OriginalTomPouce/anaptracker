<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="getRegionsSize()" class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getRegions()  }">🌎 x{{ getRegions() }} / {{ getRegionsSize() }} </span>
            <span v-else class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getRegions()  }">🌎 x{{ getRegions() }}</span>
            <span class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getTypes()  }">🔑 x{{ getTypes() }} </span>
            <span class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getBadges()  }">📛 x{{ getBadges() }} </span>

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
  name: "gDataPokepelago",
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
            getRegionsSize: function () {
                if (this.data.slot_data && this.data.slot_data.active_regions) {
                    return this.data.slot_data.active_regions.length;
                }
                return 0;
            },
            getRegions: function () {
                return this.$parent.getNumberItemsFromGroup(['Kanto Pass', 'Johto Pass', 'Hoenn Pass', 'Sinnoh Pass', 'Unova Pass', 'Kalos Pass', 'Alola Pass', 'Galar Pass', 'Hisui Pass', 'Paldea Pass']);
            },
            getTypes: function () {
                return this.$parent.getNumberItemsFromGroup(['Normal Type Key', 'Grass Type Key', 'Fire Type Key', 'Water Type Key', 'Electric Type Key', 'Flying Type Key', 'Ground Type Key', 'Rock Type Key', 'Bug Type Key', 'Fighting Type Key', 'Poison Type Key', 'Psychic Type Key', 'Ghost Type Key', 'Ice Type Key', 'Dragon Type Key', 'Steel Type Key', 'Dark Type Key', 'Fairy Type Key']);
            },
            getBadges: function () {
                return this.$parent.getNumberItemsFromName('Gym Badge');
            },
        },
  components: {
  },
};
</script>
