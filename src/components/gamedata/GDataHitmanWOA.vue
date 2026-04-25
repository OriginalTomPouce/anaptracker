<template>
    <div v-if="!isGoal('level_completion')" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
        <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Goal</div>

        <span class="mr-2 text-xs">
            <span class="font-bold" :class="{ 'opacity-25': !getNumberItemsFromName('Contract Piece')  }">
                <img v-if="isGoal('number_of_completions')" title="Completed Levels" src="/img/hitman_woa/target.png" />
                <img v-else title="Contract Pieces" src="/img/hitman_woa/goal.png" />
                x{{ getNumberItemsFromName('Contract Piece') }} 
            </span> 
            <span v-if="getGoalAmount() > 0"> 
                / {{ getGoalAmount() }}
            </span>
        </span>

    </div>

    <div v-if="isSeasonIncluded('s1')" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
        <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Hitman 1</div>
        <!-- ICA Facility, Paris, Sapienza, Marrakesh, Bangkok, Colorado, Hokkaido -->

        <img v-if="isLevelIncluded('s1', 'ica_facility')" title="ICA Facility" src="/img/hitman_woa/hitman_1/ica_facility.png" :class="{ 'opacity-25': !isLevelAvailable('ICA Facility')  }" />
        <img v-if="isLevelIncluded('s1', 'paris')" title="Paris" src="/img/hitman_woa/hitman_1/paris.png" :class="{ 'opacity-25': !isLevelAvailable('Paris')  }" />
        <img v-if="isLevelIncluded('s1', 'sapienza')" title="Sapienza" src="/img/hitman_woa/hitman_1/sapienza.png" :class="{ 'opacity-25': !isLevelAvailable('Sapienza')  }" />
        <img v-if="isLevelIncluded('s1', 'marrakesh')" title="Marrakesh" src="/img/hitman_woa/hitman_1/marrakesh.png" :class="{ 'opacity-25': !isLevelAvailable('Marrakesh')  }" />
        <img v-if="isLevelIncluded('s1', 'bangkok')" title="Bangkok" src="/img/hitman_woa/hitman_1/bangkok.png" :class="{ 'opacity-25': !isLevelAvailable('Bangkok')  }" />
        <img v-if="isLevelIncluded('s1', 'colorado')" title="Colorado" src="/img/hitman_woa/hitman_1/colorado.png" :class="{ 'opacity-25': !isLevelAvailable('Colorado')  }" />
        <img v-if="isLevelIncluded('s1', 'hokkaido')" title="Hokkaido" src="/img/hitman_woa/hitman_1/hokkaido.png" :class="{ 'opacity-25': !isLevelAvailable('Hokkaido')  }" />
    </div>

    <div v-if="isSeasonIncluded('s2')" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
        <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Hitman 2</div>
        <!-- Hawke's Bay, Miami, Santa Fortuna, Mumbai, Whittleton Creek, Isle of Sgàil, New York, Haven Island -->

        <img v-if="isLevelIncluded('s2', 'hawkes_bay')" title="Hawke's Bay" src="/img/hitman_woa/hitman_2/hawkes_bay.png" :class="{ 'opacity-25': !isLevelAvailable('Hawke\'s Bay')  }" />
        <img v-if="isLevelIncluded('s2', 'miami')" title="Miami" src="/img/hitman_woa/hitman_2/miami.png" :class="{ 'opacity-25': !isLevelAvailable('Miami')  }" />
        <img v-if="isLevelIncluded('s2', 'santa_fortuna')" title="Santa Fortuna" src="/img/hitman_woa/hitman_2/santa_fortuna.png" :class="{ 'opacity-25': !isLevelAvailable('Santa Fortuna')  }" />
        <img v-if="isLevelIncluded('s2', 'mumbai')" title="Mumbai" src="/img/hitman_woa/hitman_2/mumbai.png" :class="{ 'opacity-25': !isLevelAvailable('Mumbai')  }" />
        <img v-if="isLevelIncluded('s2', 'whittleton_creek')" title="Whittleton Creek" src="/img/hitman_woa/hitman_2/whittleton_creek.png" :class="{ 'opacity-25': !isLevelAvailable('Whittleton Creek')  }" />
        <img v-if="isLevelIncluded('s2', 'isle_of_sgail')" title="Isle of Sgàil" src="/img/hitman_woa/hitman_2/isle_of_sgail.png" :class="{ 'opacity-25': !isLevelAvailable('Isle of Sgàil')  }" />
        <img v-if="isLevelIncluded('s2_dlc', 'new_york')" title="New York" src="/img/hitman_woa/hitman_2/new_york.png" :class="{ 'opacity-25': !isLevelAvailable('New York')  }" />
        <img v-if="isLevelIncluded('s2_dlc', 'haven_island')" title="Haven Island" src="/img/hitman_woa/hitman_2/haven_island.png" :class="{ 'opacity-25': !isLevelAvailable('Haven Island')  }" />
    </div>

    <div v-if="isSeasonIncluded('s3')" :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
        <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Hitman 3</div>
        <!-- Dubai, Dartmoor, Berlin, Chongqing, Mendoza, Carpathian Mountains, Ambrose Island -->

        <img v-if="isLevelIncluded('s3', 'dubai')" title="Dubai" src="/img/hitman_woa/hitman_3/dubai.png" :class="{ 'opacity-25': !isLevelAvailable('Dubai')  }" />
        <img v-if="isLevelIncluded('s3', 'dartmoor')" title="Dartmoor" src="/img/hitman_woa/hitman_3/dartmoor.png" :class="{ 'opacity-25': !isLevelAvailable('Dartmoor')  }" />
        <img v-if="isLevelIncluded('s3', 'berlin')" title="Berlin" src="/img/hitman_woa/hitman_3/berlin.png" :class="{ 'opacity-25': !isLevelAvailable('Berlin')  }" />
        <img v-if="isLevelIncluded('s3', 'chongqing')" title="Chongqing" src="/img/hitman_woa/hitman_3/chongqing.png" :class="{ 'opacity-25': !isLevelAvailable('Chongqing')  }" />
        <img v-if="isLevelIncluded('s3', 'mendoza')" title="Mendoza" src="/img/hitman_woa/hitman_3/mendoza.png" :class="{ 'opacity-25': !isLevelAvailable('Mendoza')  }" />
        <img v-if="isLevelIncluded('s3', 'carpathian_mountains')" title="Carpathian Mountains" src="/img/hitman_woa/hitman_3/carpathian_mountains.png" :class="{ 'opacity-25': !isLevelAvailable('Carpathian Mountains')  }" />
        <img v-if="isLevelIncluded('s3', 'ambrose_island')" title="Ambrose Island" src="/img/hitman_woa/hitman_3/ambrose_island.png" :class="{ 'opacity-25': !isLevelAvailable('Ambrose Island')  }" />
    </div>
</template>

<script>
export default {
    name: "gDataHitmanWOA",
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
            levels: [
                {name: 'ICA Facility', code: "ica_facility", folder: "hitman_1"},
                {name: 'Paris', code: "paris", folder: "hitman_1"},
                {name: 'Sapienza', code: "sapienza", folder: "hitman_1"},
                {name: 'Marrakesh', code: "marrakesh", folder: "hitman_1"},
                {name: 'Bangkok', code: "bangkok", folder: "hitman_1"},
                {name: 'Colorado', code: "colorado", folder: "hitman_1"},
                {name: 'Hokkaido', code: "hokkaido", folder: "hitman_1"},
                {name: 'Hawke\'s Bay', code: "hawkes_bay", folder: "hitman_2"},
                {name: 'Miami', code: "miami", folder: "hitman_2"},
                {name: 'Santa Fortuna', code: "santa_fortuna", folder: "hitman_2"},
                {name: 'Mumbai', code: "mumbai", folder: "hitman_2"},
                {name: 'Whittleton Creek', code: "whittleton_creek", folder: "hitman_2"},
                {name: 'Isle of Sgàil', code: "isle_of_sgail", folder: "hitman_2"},
                {name: 'New York', code: "new_york", folder: "hitman_2"},
                {name: 'Haven Island', code: "haven_island", folder: "hitman_2"},
                {name: 'Dubai', code: "dubai", folder: "hitman_3"},
                {name: 'Dartmoor', code: "dartmoor", folder: "hitman_3"},
                {name: 'Berlin', code: "berlin", folder: "hitman_3"},
                {name: 'Chongqing', code: "chongqing", folder: "hitman_3"},
                {name: 'Mendoza', code: "mendoza", folder: "hitman_3"},
                {name: 'Carpathian Mountains', code: "carpathian_mountains", folder: "hitman_3"},
                {name: 'Ambrose Island', code: "ambrose_island", folder: "hitman_3"}
            ]
        };
    },
    methods: {
        /*
            Hitman: World of Assassination

            Possible Goals:
            level_completion,
            contract_collection,
            contract_collection_level_completion,
            number_of_completions
        */
        getGoalDetails: function () {
            if (!this.$parent.hasSlotData())
                return [];
            var res = [];
            var row_goal_level = { title: 'Goal', value: null, details: null };

            if (this.data.slot_data.goal_mode == 'level_completion') {
                row_goal_level.value = `Complete ${this.levels[this.data.slot_data.goal_level].name}`;
            }
            else if (this.data.slot_data.goal_mode == 'contract_collection') {
                row_goal_level.value = `Collect ${this.data.slot_data.goal_amount} contract pieces`;
            }
            else if (this.data.slot_data.goal_mode == 'contract_collection_level_completion') {
                row_goal_level.value = `Collect ${this.data.slot_data.goal_amount} contract pieces and Complete ${this.levels[this.data.slot_data.goal_level].name}`;
            }
            else if (this.data.slot_data.goal_mode == 'number_of_completions') {
                row_goal_level.value = `Complete ${this.data.slot_data.goal_amount} levels`;
            }
            else {
                row_goal_level.value = 'Unknown goal';
            }

            res.push(row_goal_level);

            return res;
        },
        getImageClass: function () {
            return this.$parent.getImageClass();
        },
        getNumberItemsFromName: function (name) {
            return this.$parent.getNumberItemsFromName(name);
        },

        isLevelAvailable: function (name) {
            if (this.isStartingLocation(name)) return true;
            return this.$parent.getNumberItemsFromName(`Level - ${name}`);
        },
        isStartingLocation: function (name) {
            if (!this.$parent.hasSlotData()) return name == 'ICA Facility'; // Default to ICA Facility if no slot data
            
            const code = this.levels.find(l => l.name == name)?.code;
            return this.data.slot_data.starting_location_name == code;
        },
        isSeasonIncluded: function (season) {
            if (!this.$parent.hasSlotData())
                return true;
            if (season == 's2') {
                return (this.data.slot_data[`included_s2_locations`] && 
                        this.data.slot_data[`included_s2_locations`].length > 0) || (
                        this.data.slot_data[`included_s2_dlc_locations`] && 
                        this.data.slot_data[`included_s2_dlc_locations`].length > 0);
            }
            return this.data.slot_data[`included_${season}_locations`] && this.data.slot_data[`included_${season}_locations`].length > 0;
        },
        isLevelIncluded: function (season, level_code) {
            //console.log(this);
            
            if (!this.$parent.hasSlotData())
                return true;
            
            return this.data.slot_data[`included_${season}_locations`]?.includes(level_code);
        },
        isGoal(goal) {
            if (!this.$parent.hasSlotData())
                return goal == 'contract_collection';
            return this.data.slot_data.goal_mode == goal;
        },
        getGoalAmount() {
            if (!this.$parent.hasSlotData())
                return 0;
            return this.data.slot_data.goal_amount;
        }
    }
}
</script>