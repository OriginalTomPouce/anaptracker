<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

            <span v-if="getGoalPieces()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getPieces()  }">🧩 x{{ getPieces() }} </span> / {{ getGoalPieces() }}</span>
            <span v-else class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getPieces()  }">🧩 x{{ getPieces() }} </span>

        </div>
    </div>
</template>
    
<script>

/**
* JigSaw
* 
* Count puzzle pieces and win.
*/ 
export default {
  name: "gDataJigsaw",
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
            countPuzzlePieces: function (name) {
                var res = 0;
                var game_data = this.$parent.get_game_data();
                if (game_data && game_data.item_name_groups) {

                    var group = game_data.item_name_groups[name];
                    var list_of_ids = [];

                    if (!group) // For Old APworld compatiblity
                        return 0;

                    for (var x = 0; x < group.length; x++) {
                        list_of_ids.push(game_data.item_name_to_id[group[x]]);
                    }
                    for (var x = 0; x < this.data.tracker_data.player_items_received.length; x++) {
                        if (list_of_ids.includes(this.data.tracker_data.player_items_received[x][0])) {
                            for (const property in game_data.item_name_to_id) {
                                if (game_data.item_name_to_id[property] == this.data.tracker_data.player_items_received[x][0]) {
                                    var tabl = property.split(' ');
                                    res += parseInt(tabl);
                                }
                            }
                        }
                    }
                }
                return res;
            },
            getGoalPieces: function () {
                if (this.data.slot_data.piece_order) {
                    return this.data.slot_data.piece_order.length;
                }
                return 0;
            },
            getPieces: function () {
                if (this.$parent.hasSlotData()) {
                    var puule = this.countPuzzlePieces('Puzzle Pieces');
                    return puule;
                }
                return 0;
                
            },
        },
  components: {
  },
};
</script>
