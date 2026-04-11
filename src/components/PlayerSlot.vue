<template>
    <div v-if="displayable()" @mouseover="hoverOn()" @mouseleave="hoverOff()" :class=" { 'bg-cyan-200' : get_status() == 30, 'py-1' : $parent.$parent.OPTIONS.row_size == 1,  'text-sm py-1' : !$parent.$parent.OPTIONS.row_size, 'text-lg py-2' : $parent.$parent.OPTIONS.row_size == 2 }" class="relative inline-block w-full tracker-history leading-5 font-semibold font-xl h-full px-2 border-t-2 border-t-gray-900">
        <div :class="getSpeedBarClass()" class="absolute left-0 top-0 bottom-0 z-1" :style="{ 'width' : str_percent_completion() }"></div>
        <div v-if="mHover" class="absolute left-0 right-0 top-0 bottom-0 z-1 bg-gray-100/30"></div>
        <div @click="toggleExpand()" class="z-2 flex flex-column justify-between">
            <div class="w-1/4 lg:w-1/5 2xl:w-1/6 z-3 text-dark " :class="{ 'opacity-50' : get_status() == 0 }">
                <span v-if="slotLocked()">🔒</span>
                <a @click="toggleExpand()" :href="slotURL()" target="_blank" class="mr-2 font-bold hover:text-blue-800 hover:underline">
                    <span v-if="$parent.$parent.OPTIONS.show_slot_number" class="font-bold">{{ data.id }} - </span>{{ player_name }}
                </a>
                <br v-if="$parent.$parent.OPTIONS.row_size" />
                <span class="font-normal text-tiny">({{ player_game }})</span>
            </div>
            <div class="w-1/2 lg:w-3/5 2xl:w-4/6 z-3 text-sm">
                <div class="clear-both text-center font-normal">


                    <div v-if="displayHints() && getImportantRecievedHints()" :class="getImageClass()" class="inline-block bg-amber-200/60 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
                        <div v-if="get_size()" class="text-xs font-normal text-left">Hints</div>

                        <span v-if="getImportantRecievedHints() > 5" class="mr-2 text-xs font-bold"><img title="Hinted Item on their world" src="/img/event.png" />x{{ getImportantRecievedHints() }} </span>
                        <span v-else class="text-xs font-bold">
                            <img v-if="getImportantRecievedHints() > 4" title="Hinted Item on their world" src="/img/event.png" />
                            <img v-if="getImportantRecievedHints() > 3" title="Hinted Item on their world" src="/img/event.png" />
                            <img v-if="getImportantRecievedHints() > 2" title="Hinted Item on their world" src="/img/event.png" />
                            <img v-if="getImportantRecievedHints() > 1" title="Hinted Item on their world" src="/img/event.png" />
                            <img title="Hinted Item on their world" src="/img/event.png" />
                        </span>
                    </div>
                    <div v-if="displayHints() && getImportantSentHints()" :class="getImageClass()" class="inline-block bg-cyan-200/60 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
                        <div v-if="get_size()" class="text-xs font-normal text-left">Hints</div>

                        <span v-if="getImportantSentHints() > 5" class="mr-2 text-xs font-bold"><img title="Hint sent to another player" src="/img/unknown.png" />x{{ getImportantSentHints() }} </span>
                        <span v-else class="text-xs font-bold">
                            <img v-if="getImportantSentHints() > 4" title="Hint sent to another player" src="/img/unknown.png" />
                            <img v-if="getImportantSentHints() > 3" title="Hint sent to another player" src="/img/unknown.png" />
                            <img v-if="getImportantSentHints() > 2" title="Hint sent to another player" src="/img/unknown.png" />
                            <img v-if="getImportantSentHints() > 1" title="Hint sent to another player" src="/img/unknown.png" />
                            <img title="Hint sent to another player" src="/img/unknown.png" />
                        </span>
                    </div>

                    <component :is="get_game_data_class()"
                               v-bind:data="data"
                               v-bind:index="index"
                               v-bind:gamedata="get_game_data()"
                               ref="slot_tracker" />
                    <div v-if="hasDatapackage() && data.extended" class="block relative">
                        <div v-if="$refs.slot_tracker && $refs.slot_tracker.getGoalDetails().length" class="inline-block w-full align-top p-[2px] pl-[4px] pt-[4px]">
                            <div class="bg-emerald-200/60 rounded-xs p-[2px] pl-[4px] pt-[4px] mx-2 bg-opacity-25 text-xs">
                                <ul>
                                    <li v-for="(element, index) in $refs.slot_tracker.getGoalDetails()">
                                        {{ element.title }} <span v-if="element.value"> : <span class="font-bold"> {{ element.value }}</span></span> <span v-if="element.details">({{ element.details }})</span>
                                    </li>
                                </ul>
                            </div>
                        </div>
                        <div class="inline-block w-1/2 align-top p-[2px] pl-[4px] pt-[4px]">
                            <div class="bg-amber-200/60 rounded-xs p-[2px] pl-[4px] pt-[4px] mx-2 bg-opacity-25 text-xs">
                                Hinted Locations :
                                <ul class="list-disc list-inside">
                                    <li v-for="(element, index) in getImportantRecievedHintsList()">
                                        <span class="font-bold">{{ getLocationName(element[2]) }}</span> {{ $parent.getItemHinted(element) }}

                                    </li>
                                </ul>
                            </div>
                        </div>
                        <div class="inline-block w-1/2 align-top p-[2px] pl-[4px] pt-[4px]">
                            <div class="bg-cyan-200/60 rounded-xs p-[2px] pl-[4px] pt-[4px] mx-2 bg-opacity-25 text-xs">
                                Hinted Items :
                                <ul class="list-disc list-inside">
                                    <li v-for="(element, index) in getImportantSentHintsList()">
                                        <span class="font-bold">{{ getItemName(element[3]) }}</span> {{ $parent.getLocationHinted(element) }}

                                    </li>
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="w-1/4 lg:w-1/5 2xl:w-1/6 z-3 text-right">
                <span v-if="$parent.$parent.OPTIONS.show_timer" class="font-bold
                      text-tiny mr-3">{{ get_last_activity() }}</span>
                <span class="font-normal" v-if="$parent.$parent.OPTIONS.sort_by == 4">
                    <span class="font-bold">{{ get_total_checks() - get_current_checks() }}</span> left
                </span>
                <span v-else>
                    <span v-if="!$parent.$parent.OPTIONS.row_size" class="font-normal text-tiny mr-2">({{ percent_completion() }}%)</span><span class="font-bold">{{ get_current_checks() }}</span> / {{ get_total_checks() }}<br /><span v-if="$parent.$parent.OPTIONS.row_size" class="font-normal text-tiny">({{ percent_completion() }}%)</span>
                </span>
            </div>
        </div>
    </div>
</template>

<script>

    import GData from './gamedata/GData.vue';
    import { markRaw } from 'vue'
    import  LIST_OF_GAMES from "../listofgames.js";


    export default {
        name: "playerSlot",
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
                LIST_OF_GAMES: markRaw(LIST_OF_GAMES),
                mHover: 0
            };
        },

        methods: {
            hoverOn: function () {
                this.mHover = 1;
            },
            hoverOff: function () {
                this.mHover = 0;
            },
            hasSlotData: function () {
                if (Object.keys(this.data.slot_data).length) {
                    return true;
                }
                return false;
            },
            supportedGame: function () {
                for (var x = 0; x < this.LIST_OF_GAMES.length; x++) {
                    if (this.LIST_OF_GAMES[x].name == this.player_game) {
                        return true;
                    }
                }
                return false;
            },
            hasDatapackage: function () {
                if (this.get_game_data())
                    return true;
                return false;
            },
            getSpeedBarClass: function () {
                if (this.$parent.$parent.OPTIONS.show_speed && this.data.locations_hist.length > 1 && this.data.total_locations > 0) {
                    var first = this.data.locations_hist[0];
                    var last = this.data.locations_hist[this.data.locations_hist.length - 1];
                    var speeeeeed = 100 * (last - first) / this.data.total_locations;

                    if (speeeeeed > 15)
                        return 'bg-linear-to-r from-rose-200 to-green-500';
                    if (speeeeeed > 10)
                        return 'bg-linear-to-r from-red-200 to-green-500';
                    if (speeeeeed > 7)
                        return 'bg-linear-to-r from-red-300 to-green-500';
                    if (speeeeeed > 5)
                        return 'bg-linear-to-r from-orange-300 to-green-500';
                    //if (speeeeeed > 2)
                    //    return 'bg-linear-to-r from-amber-300 to-green-500';
                    if (speeeeeed > 3)
                        return 'bg-linear-to-r from-yellow-300 to-green-500';
                    if (speeeeeed > 2)
                        return 'bg-linear-to-r from-lime-300 to-green-500';
                    if (speeeeeed > 1)
                        return 'bg-linear-to-r from-green-300 to-green-500';
                    if (speeeeeed > 0.2)
                        return 'bg-linear-to-r from-green-400 to-green-500';
                }

                return 'bg-green-500';
            },
            getImageClass: function () {
                if (this.$parent.$parent.OPTIONS.row_size == 2) {
                    return 'iconbar-L my-1';
                }
                else if (this.$parent.$parent.OPTIONS.row_size == 1) {
                    return 'iconbar-M';
                }
                return 'iconbar-S';
            },
            getNumberItemsFromName: function (name) {
                var res = 0;
                var game_data = this.get_game_data();
                if (game_data && game_data.item_name_to_id) {
                    var id = game_data.item_name_to_id[name];
                    for (var x = 0; x < this.data.tracker_data.player_items_received.length; x++) {
                        if (this.data.tracker_data.player_items_received[x][0] == id)
                            res++;
                    }
                }
                return res;
            },
            getNumberItemsFromGroup: function (names) {
                var res = 0;
                var game_data = this.get_game_data();
                if (game_data && game_data.item_name_to_id) {
                    var bottle_array = []
                    for (var x = 0; x < names.length; x++) {
                        bottle_array.push(game_data.item_name_to_id[names[x]]);
                    }
                    for (var x = 0; x < this.data.tracker_data.player_items_received.length; x++) {
                        if (bottle_array.includes(this.data.tracker_data.player_items_received[x][0]))
                            res++;
                    }
                }
                return res;
            },
            getNumberItemsFromCategory: function (name) {
                var res = 0;
                var game_data = this.get_game_data();
                if (game_data && game_data.item_name_groups) {

                    var group = game_data.item_name_groups[name];
                    var list_of_ids = [];

                    if (!group) // For Old APworld compatiblity
                        return 0;

                    for (var x = 0; x < group.length; x++) {
                        list_of_ids.push(game_data.item_name_to_id[group[x]]);
                    }
                    for (var x = 0; x < this.data.tracker_data.player_items_received.length; x++) {
                        if (list_of_ids.includes(this.data.tracker_data.player_items_received[x][0]))
                            res++;
                    }
                }
                return res;
            },
            getNumberItemsNameStart: function (name) {
                var res = 0;
                var game_data = this.get_game_data();
                if (game_data && game_data.location_name_to_id) {
                    var bottle_array = [];
                    for (var key in game_data.item_name_to_id) {
                        if (key.startsWith(name)) {
                            bottle_array.push(game_data.item_name_to_id[key]);
                        }
                    }
                    for (var x = 0; x < this.data.tracker_data.player_items_received.length; x++) {
                        if (bottle_array.includes(this.data.tracker_data.player_items_received[x][0]))
                            res++;
                    }
                }
                return res;
            },
            matchesResearch: function () {
                if (this.$parent.$parent.GLOBAL_TRACKER_DATA.text_filter == '')
                    return true;
                if (this.data.game.toLowerCase().includes(this.$parent.$parent.GLOBAL_TRACKER_DATA.text_filter.toLowerCase()) || this.data.name.toLowerCase().includes(this.$parent.$parent.GLOBAL_TRACKER_DATA.text_filter.toLowerCase()))
                    return true;
                return false;
            },
            displayable: function () {
                if (((this.$parent.$parent.OPTIONS.show_done || this.get_time_diff() < (600)) || this.data.tracker_data.status < 30) && this.matchesResearch()) {
                    return true;
                }
                return false;
            },
            displayHints: function () {
                return !this.data.extended && this.$parent.$parent.OPTIONS.show_hints;
            },
            get_game_data_class: function () {
                for (var x = 0; x < this.LIST_OF_GAMES.length; x++) {
                    if (this.LIST_OF_GAMES[x].name == this.player_game) {
                        return this.LIST_OF_GAMES[x].class;
                    }
                }

                return GData;
            },
            get_game_data: function () {
                if (this.player_game) {
                    return this.gamedata[this.player_game];
                }
                return null;
            },
            get_status: function () {
                // On reprend le statut du joueur ?
                //
                // 0 - Online
                // 1 - Playing
                // 5 - Offline
                // 30 - Game Completed
                if (this.data.tracker_data.status >= 30)
                    return 30;
                return this.data.tracker_data.status;
            },
            get_size: function () {
                return this.$parent.$parent.OPTIONS.row_size;
            },
            get_current_checks: function () {
                return this.data.tracker_data.player_checks_done.length;
            },
            get_total_checks: function () {
                return this.data.total_locations;
            },
            percent_completion: function () {
                var total_checks = this.get_total_checks();
                if (total_checks > 0)
                    return Math.round(this.get_current_checks() * 10000 / total_checks) / 100;
                return 0;
            },
            str_percent_completion: function () {
                var total_checks = this.get_total_checks();
                if (total_checks > 0 && this.get_status() < 30)
                    return (Math.floor(this.get_current_checks() * 10000 / total_checks) / 100).toString() + '%';
                return 0;
            },
            get_time_diff: function () {
                if (this.data.tracker_data.activity_timer != '') {
                    var date_now = Date.now();
                    var date_act = new Date(this.data.tracker_data.activity_timer).getTime();
                    return Math.floor((date_now - date_act) / 1000);

                }
                return 0;
            },
            get_last_activity: function () {
                var time = this.get_time_diff();

                if (time > 3600 * 24) {
                    return (Math.floor(time / (360 * 24)) / 10).toString() + 'D';
                }
                else if (time > 3600) {
                    return (Math.floor(time / (360)) / 10).toString() + 'H';
                }
                else if (time > 900) {
                    return (Math.floor(time / (60))).toString() + 'm';
                }

                return '';
            },
            toggleExpand: function () {
                if (this.data.extended) {
                    this.data.extended = 0;
                }
                else {
                    this.data.extended = 1;
                    if (!this.hasDatapackage()) {
                        this.$parent.$parent.requestDataPackage(this.data.game);
                    }
                }
            },
            /**
             * 0 : Player who send the hint
             * 1 : Player who recieve the hint
             * 2 : Location
             * 3 : Item
             * 4 : found ?
             * 5 : Entrance Label
             * 6 : Item classification
             * 7 : Hint classification (???, Non-important, Avoid, Important, Found)
             *
             */
            getImportantSentHints: function () {
                var res = 0;
                for (var x = 0; x < this.data.tracker_data.hints.length; x++) {
                    if (this.data.tracker_data.hints[x][0] == this.data.id && (this.data.tracker_data.hints[x][6] == 1 || this.data.tracker_data.hints[x][7] == 30) && this.data.tracker_data.hints[x][4] == false)
                        res++;
                }
                return res;
            },
            getImportantRecievedHints: function () {
                var res = 0;
                for (var x = 0; x < this.data.tracker_data.hints.length; x++) {
                    if (this.data.tracker_data.hints[x][1] == this.data.id && (this.data.tracker_data.hints[x][6] == 1 || this.data.tracker_data.hints[x][7] == 30) && this.data.tracker_data.hints[x][4] == false)
                        res++;
                }
                return res;
            },
            getImportantSentHintsList: function () {
                var res = [];
                for (var x = 0; x < this.data.tracker_data.hints.length; x++) {
                    if (this.data.tracker_data.hints[x][0] == this.data.id && (this.data.tracker_data.hints[x][6] == 1 || this.data.tracker_data.hints[x][7] == 30) && this.data.tracker_data.hints[x][4] == false)
                        res.push(this.data.tracker_data.hints[x]);
                }
                return res;
            },
            getImportantRecievedHintsList: function () {
                var res = [];
                for (var x = 0; x < this.data.tracker_data.hints.length; x++) {
                    if (this.data.tracker_data.hints[x][1] == this.data.id && (this.data.tracker_data.hints[x][6] == 1 || this.data.tracker_data.hints[x][7] == 30) && this.data.tracker_data.hints[x][4] == false)
                        res.push(this.data.tracker_data.hints[x]);
                }
                return res;
            },
            getLocationName: function (id) {
                var game_data = this.get_game_data();
                if (game_data && game_data.location_name_to_id) {
                    return Object.keys(game_data.location_name_to_id).find(key => game_data.location_name_to_id[key] === id);
                }
                return '???';

            },
            getItemName: function (id) {
                var game_data = this.get_game_data();
                if (game_data && game_data.item_name_to_id) {
                    return Object.keys(game_data.item_name_to_id).find(key => game_data.item_name_to_id[key] === id);
                }
                return '???';

            },
            slotURL: function () {
                var linkURL = this.$parent.$parent.webhostValue(this.$parent.$parent.WEBHOST_USED).apurl;

                linkURL += "/tracker/" + this.$parent.$parent.TRACKER_ID + "/0/" + this.data.id;
                return linkURL;
            },
            slotLocked: function () {
                if (this.$parent.getSlotLockCheck(this.data.name))
                    return false;
                return true;
            }
        },
        components: {
            GData
        },
    };
</script>
