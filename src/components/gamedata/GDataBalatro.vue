<template>
    <div class="inline-block">

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Decks</div>
            <span v-if="jockerGoal()" class="mr-2 text-xs"><span class="font-bold" :class="{ 'opacity-25': !getJokerCards()  }"><img title="Joker" src="/img/balatro/joker.png" />x{{ getJokerCards() }} </span> / {{ jockerGoal() }}</span>
            <span v-if="jockerGoal()" class="mr-2"></span>

            <img v-if="stakeExists(1, 'White Stake')" title="White Stake" src="/img/balatro/white_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('White Stake')  }" />
            <img v-if="stakeExists(2, 'Red Stake')" title="Red Stake" src="/img/balatro/red_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('Red Stake')  }" />
            <img v-if="stakeExists(3, 'Green Stake')" title="Green Stake" src="/img/balatro/green_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('Green Stake')  }" />
            <img v-if="stakeExists(4, 'Black Stake')" title="Black Stake" src="/img/balatro/black_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('Black Stake')  }" />
            <img v-if="stakeExists(5, 'Blue Stake')" title="Blue Stake" src="/img/balatro/blue_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('Blue Stake')  }" />
            <img v-if="stakeExists(6, 'Purple Stake')" title="Purple Stake" src="/img/balatro/purple_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('Purple Stake')  }" />
            <img v-if="stakeExists(7, 'Orange Stake')" title="Orange Stake" src="/img/balatro/orange_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('Orange Stake')  }" />
            <img v-if="stakeExists(8, 'Gold Stake')" title="Gold Stake" src="/img/balatro/gold_stake.png" :class="{ 'opacity-25': !getNumberItemsFromName('Gold Stake')  }" />
            <span v-if="stakeGoal()" class="mr-2"></span>

            <img v-if="deckExists('b_blue')" title="Blue Deck" src="/img/balatro/blue_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Blue Deck')  }" />
            <img v-if="deckExists('b_red')" title="Red Deck" src="/img/balatro/red_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Red Deck')  }" />
            <img v-if="deckExists('b_yellow')" title="Yellow Deck" src="/img/balatro/yellow_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Yellow Deck')  }" />
            <img v-if="deckExists('b_green')" title="Green Deck" src="/img/balatro/green_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Green Deck')  }" />
            <img v-if="deckExists('b_black')" title="Black Deck" src="/img/balatro/black_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Black Deck')  }" />
            <img v-if="deckExists('b_magic')" title="Magic Deck" src="/img/balatro/magic_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Magic Deck')  }" />
            <img v-if="deckExists('b_nebula')" title="Nebula Deck" src="/img/balatro/nebula_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Nebula Deck')  }" />
            <img v-if="deckExists('b_ghost')" title="Ghost Deck" src="/img/balatro/ghost_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Ghost Deck')  }" />
            <img v-if="deckExists('b_abandoned')" title="Abandoned Deck" src="/img/balatro/abandoned_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Abandoned Deck')  }" />
            <img v-if="deckExists('b_checkered')" title="Checkered Deck" src="/img/balatro/checkered_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Checkered Deck')  }" />
            <img v-if="deckExists('b_zodiac')" title="Zodiac Deck" src="/img/balatro/zodiac_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Zodiac Deck')  }" />
            <img v-if="deckExists('b_painted')" title="Painted Deck" src="/img/balatro/painted_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Painted Deck')  }" />
            <img v-if="deckExists('b_anaglyph')" title="Anaglyph Deck" src="/img/balatro/anaglyph_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Anaglyph Deck')  }" />
            <img v-if="deckExists('b_plasma')" title="Plasma Deck" src="/img/balatro/plasma_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Plasma Deck')  }" />
            <img v-if="deckExists('b_erratic')" title="Erratic Deck" src="/img/balatro/erratic_deck.png" :class="{ 'opacity-25': !getNumberItemsFromName('Erratic Deck')  }" />

        </div>

        <div :class="getImageClass()" class="inline-block bg-stone-100/40 rounded-xs p-[2px] pl-[4px] pb-[4px] mx-2 bg-opacity-25">
            <div v-if="$parent.get_size()" class="text-xs font-normal text-left">Content</div>


            <span v-if="!jockerGoal()" class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getJokerCards()  }"><img title="Joker Cards" src="/img/balatro/joker.png" />x{{ getJokerCards() }} </span>
            <span class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getPlanetCards()  }"><img title="Planet Cards" src="/img/balatro/planet.png" />x{{ getPlanetCards() }} </span>
            <span class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getSpectralCards()  }"><img title="Spectral Cards" src="/img/balatro/spectral.png" />x{{ getSpectralCards() }} </span>
            <span class="mr-2 text-xs font-bold" :class="{ 'opacity-25': !getTarotCards()  }"><img title="Tarot Cards" src="/img/balatro/tarot.png" />x{{ getTarotCards() }} </span>

        </div>
    </div>
</template>
    
<script>

/**
* Balatro
* 
* Goal is either to beat the ante (number of deck, or specifics conditions), or get a certain amount of Jokers
* You also need at least the Upper Key (depending on Key settings).
* 
* Goal Setting :
* 0 - Beat with a specific number Decks
* 1 - Unlock Jockets
* 2 - Beat Ante
* 3 - Beat Decks on specific stake
* 4 - Win with specifics jokers on stake
* 5 - Beat with a specific combinaison of decks and stakes
*/ 
export default {
  name: "gDataBalatro",
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
                var row_goal = { title: 'Goal', value: null, details: null };
                var row_requirement = { title: 'Number of decks to beat', value: null, details: null };
                var row_requirement2 = { title: 'Minimum Stake', value: null, details: null };

                if (this.data.slot_data.goal == 0) {
                    row_goal.value = 'Beat Decks';
                    row_requirement.value = this.data.slot_data.decks_win_goal;
                }
                else if (this.data.slot_data.goal == 1) {
                    row_goal.value = 'Unlock Jokers';
                    row_requirement.title = 'Jokers to collect';
                    row_requirement.value = this.data.slot_data.jokers_unlock_goal;
                }
                else if (this.data.slot_data.goal == 2) {
                    row_goal.value = 'Beat Ante';
                    row_requirement.title = 'Ante';
                    row_requirement.value = this.data.slot_data.ante_win_goal;
                }
                else if (this.data.slot_data.goal == 3) {
                    row_goal.value = 'Beat decks on stake';
                    row_requirement.value = this.data.slot_data.decks_win_goal;
                    if (this.data.slot_data.hasOwnProperty('required_stake_for_goal'))
                        row_requirement2.value = this.data.slot_data.required_stake_for_goal.join(', ');
                }
                else if (this.data.slot_data.goal == 4) {
                    row_goal.value = 'Win with Jokers on stake';
                    row_requirement.title = 'Jokers to collect';
                    row_requirement.value = this.data.slot_data.joker_goal;
                    if (this.data.slot_data.hasOwnProperty('required_stake_for_goal'))
                        row_requirement2.value = this.data.slot_data.required_stake_for_goal.join(', ');
                }
                else if (this.data.slot_data.goal == 5) {
                    row_goal.value = 'Beat Unique Decks';
                    row_requirement.title = 'Number of decks/stakes combinaisons to beat';
                    row_requirement.value = this.data.slot_data.unique_deck_win_goal;
                }
                else if (this.data.slot_data.goal == 6) {
                    row_goal.value = 'Clear Challenges';
                    row_requirement.title = 'Number of challenges to clear';
                    row_requirement.value = this.data.slot_data.number_of_challenges_for_goal;
                }

                res.push(row_goal);
                res.push(row_requirement);
                if (row_requirement2.value)
                    res.push(row_requirement2);


                return res;
            },
            getImageClass: function () {
                return this.$parent.getImageClass();
            },
            getNumberItemsFromName: function (name) {
                return this.$parent.getNumberItemsFromName(name);
            },
            getNumberItemsFromCategory: function (name) {
                return this.$parent.getNumberItemsFromCategory(name);
            },
            getJokerCards: function () {
                var res = 0;
                if (this.$parent.hasSlotData() && this.data.slot_data.jokerbundles.length > 0)
                    res += this.$parent.getNumberItemsNameStart('Joker Bundle') * this.data.slot_data.jokerbundles[0].length;
                return res + this.getNumberItemsFromCategory('Joker');
            },
            getTarotCards: function () {
                if (this.getNumberItemsFromName('Tarot Bundle'))
                    return 23;
                return this.getNumberItemsFromCategory('Tarot');
            },
            getSpectralCards: function () {
                if (this.getNumberItemsFromName('Spectral Bundle'))
                    return 19;
                return this.getNumberItemsFromCategory('Spectral');
            },
            getPlanetCards: function () {
                if (this.getNumberItemsFromName('Planet Bundle'))
                    return 13;
                return this.getNumberItemsFromCategory('Planet');
            },
            deckExists: function (name) {
                if (this.data.slot_data.hasOwnProperty('included_decks') && this.data.slot_data.included_decks.length > 0)
                    return this.data.slot_data.included_decks.includes(name);
                return true;
            },
            stakeExists: function (id, name) {
                if (this.data.slot_data.hasOwnProperty('included_stakes') && this.data.slot_data.included_stakes.length > 0)
                    return this.data.slot_data.included_stakes.includes(id);
                return this.getNumberItemsFromName(name);
            },
            jockerGoal: function () {
                if (this.data.slot_data.hasOwnProperty('goal') && this.data.slot_data.goal == 1)
                    return this.data.slot_data.jokers_unlock_goal;
                return false;
                
            },
            stakeGoal: function () {
                if (this.data.slot_data.hasOwnProperty('goal') && [3,5].includes(this.data.slot_data.goal))
                    return true;
                return this.$parent.getNumberItemsFromGroup(['White Stake', 'Red Stake', 'Green Stake', 'Black Stake', 'Blue Stake', 'Purple Stake', 'Orange Stake', 'Gold Stake']);

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
