<template>
    <div class="flex flex-col bg-gray-500 max-w-50vh">
        <div class=" divide-solid divide-gray-900">
            <PlayerSlot v-for="(element, index) in sorted_players()"
                        :key="'owel-' + index"
                        v-bind:index="index"
                        v-bind:player_name="element.name"
                        v-bind:player_game="element.game"
                        v-bind:gamedata="gamedata"
                        v-bind:data="element"
                        shallowRef="player_slot">
            </PlayerSlot>
        </div>
        <div :class=" { 'bg-cyan-200' : get_state() > 1, 'py-6' : $parent.OPTIONS.row_size,  'text-sm py-4' : !$parent.OPTIONS.row_size  }" class="relative inline-block w-full tracker-history text-xl leading-5 font-semibold font-xl h-full px-2 border-t-2 border-t-gray-900">
            <div class="absolute left-0 top-0 bottom-0 z-1 bg-green-500" :style="{ 'width' : str_percent_completion() }"></div>
            <div class="z-2 flex flex-column justify-between text-lg items-center ">
                <div class="w-1/2 z-3 text-lg">

                    <div v-if="get_state() > 1" class="mr-2" :class="{'text-2xl':  $parent.OPTIONS.row_size == 2, 'text-xl':  $parent.OPTIONS.row_size == 1}">DONE ! Congratulations !</div>
                    <div v-else class="mr-2 align-middle" :class="{'text-2xl':  $parent.OPTIONS.row_size == 2, 'text-xl':  $parent.OPTIONS.row_size == 1}">Games completed : {{ games_completed() }} / {{ total_games() }}</div>
                </div>

                <div :class="{'text-2xl':  $parent.OPTIONS.row_size == 2, 'text-xl':  $parent.OPTIONS.row_size == 1}" class="w-1/2 z-3 text-right"><span v-if="!$parent.OPTIONS.row_size" class="font-normal text-tiny mr-2">({{ percent_completion() }}%)</span>{{ get_current_checks() }} / {{ get_total_checks() }}<br /><span v-if="$parent.OPTIONS.row_size" class="font-normal text-tiny">({{ percent_completion() }}%)</span></div>
            </div>
        </div>

    </div>
</template>

<script>


    import PlayerSlot from './PlayerSlot.vue';
    export default {
        name: 'playerList',
        props: {
            globaldata: Object,
            gamedata: Object
        },
        data: function () {
            return {
                showMenu: false,
                hide_done: true,
                done_stuff: function () {
                    if (this.$parent.removeOnCompleted)
                        return "Hidden";
                    return "Shown";
                }
            }
        },

        methods: {
            sorted_players: function () {
                if (this.$parent.OPTIONS.sort_by == 1) {
                    return this.globaldata.players.sort((a, b) => a.tracker_data.player_checks_done.length - b.tracker_data.player_checks_done.length);
                }
                if (this.$parent.OPTIONS.sort_by == 2) {
                    return this.globaldata.players.sort((a, b) => (a.tracker_data.player_checks_done.length / a.total_locations) - (b.tracker_data.player_checks_done.length / b.total_locations));
                }
                if (this.$parent.OPTIONS.sort_by == 3) {
                    return this.globaldata.players.sort((a, b) => a.total_locations - b.total_locations);
                }
                if (this.$parent.OPTIONS.sort_by == 4) {
                    return this.globaldata.players.sort((a, b) => (b.total_locations - b.tracker_data.player_checks_done.length) - (a.total_locations - a.tracker_data.player_checks_done.length));
                }
                if (this.$parent.OPTIONS.sort_by == 5) {
                    return this.globaldata.players.sort((a, b) => (b.tracker_data.player_checks_done.length / b.total_locations) - (a.tracker_data.player_checks_done.length / a.total_locations));
                }
                if (this.$parent.OPTIONS.sort_by == 6) {
                    return this.globaldata.players.sort((a, b) => a.tracker_data.activity_timer.localeCompare(b.tracker_data.activity_timer));
                }
                if (this.$parent.OPTIONS.sort_by == 7) {
                    return this.globaldata.players.sort((a, b) => a.game.localeCompare(b.game));
                }
                return this.globaldata.players;
            },
            games_completed: function () {
                var res = 0;
                for (var x = 0; x < this.globaldata.players.length; x++) {
                    if (this.globaldata.players[x].tracker_data.status >= 30)
                        res++;
                }
                return res;
            },
            total_games: function () {
                return this.globaldata.players.length;
            },
            toggleNavbar: function () {
                this.showMenu = !this.showMenu;
            },
            saveTracker: function () {
                this.$parent.saveTracker();
            },
            resetTracker: function () {
                this.$parent.resetTracker();
            },
            get_state: function () {
                if (this.get_current_checks() == this.get_total_checks()) {
                    return 2;
                }
                return 0;
            },
            get_current_checks: function () {
                return this.globaldata.total_checks_done;
            },
            get_total_checks: function () {
                var res = 0;
                for (var x = 0; x < this.globaldata.players.length; x++) {
                    res += this.globaldata.players[x].total_locations;
                }
                return res;
            },
            percent_completion: function () {
                var total_checks = this.get_total_checks();
                if (total_checks > 0)
                    return Math.round(this.get_current_checks() * 10000 / total_checks) / 100;
                return 0;
            },
            str_percent_completion: function () {
                var total_checks = this.get_total_checks();
                if (total_checks > 0 && this.get_state() < 2)
                    return (Math.floor(this.get_current_checks() * 10000 / total_checks) / 100).toString() + '%';
                return 0;
            },
            getPlayerbyID: function (id) {
                var players = this.globaldata.players;
                for (var x = 0; x < players.length; x++) {
                    if (players[x].id == id)
                        return players[x];
                }
                return null;
            },
            getItemHinted: function (element) {
                var player = this.getPlayerbyID(element[0]);
                var datapackage = this.gamedata[player.game];

                if (typeof datapackage !== 'object')
                    return '(??? for ' + player.name + ')';

                for (var key in datapackage.item_name_to_id) {
                    if (datapackage.item_name_to_id[key] == element[3])
                        return '(' + key + ' for ' + player.name + ')';
                }

                return '(??? for ' + player.name + ')';
            },
            getLocationHinted: function (element) {
                var player = this.getPlayerbyID(element[1]);
                var datapackage = this.gamedata[player.game];

                if (typeof datapackage !== 'object')
                    return '(??? from ' + player.name + ')';

                for (var key in datapackage.location_name_to_id) {
                    if (datapackage.location_name_to_id[key] == element[2])
                        return '(' + key + ' from ' + player.name + ')';
                }

                return '(??? from ' + player.name + ')';

            },
            getSlotLockCheck: function (name) {
                if (this.globaldata.slotlock == 0)
                    return true;

                console.log(this.globaldata.slotlock);
                var needle = "Unlock " + name;
                var needle_id = 0;
                var player = this.getPlayerbyID(this.globaldata.slotlock);
                var datapackage = this.gamedata[player.game];

                if (datapackage.item_name_to_id[needle])
                    needle_id = datapackage.item_name_to_id[needle];
                for (var x = 0; x < player.tracker_data.player_items_received.length; x++) {
                    if (player.tracker_data.player_items_received[x][0] == needle_id)
                        return true;
                }
                return false;

            },
        },
        components: {
            PlayerSlot,
        }
    }
</script>
