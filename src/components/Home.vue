<template>
    <div class="text-center text-white">
        <h1 class="text-2xl my-4">Welcome to A Normal AP Tracker !</h1>
        <div class="mt-4 mb-10 p-6 align-top">

            <span class="text-lg">Please enter the ID or the URL of the Archipelago Room.</span>
            <form @submit.prevent="loadRoom()">
                <input v-model="roomid" type="text" class="border-1 border-gray-500 rounded-xs p-2 mr-2 text-lg" />
                <input type="submit" class="bg-blue-800 p-2 br-1 rounded-xs text-lg" value="Track !" />
            </form>
            <div v-if="error" class="text-red-400 font-bold mt-2">The URL or the room ID is unrecognized.</div>
        </div>
        <div class="inline-block w-100 p-6 align-top">
            <span class="font-bold text-lg">What the app can do :</span>
            <ul class="list-disc">
                <li>
                    Track global check completion and individual checks completion. (like the usual tracker)
                </li>
                <li>
                    Display key items for supported games.
                </li>
                <li>
                    Size settings, and display options.
                </li>
                <li>
                    List sorting (by completion, activity, ...)
                </li>
            </ul>
        </div>
        <div class="inline-block w-100 p-6 align-top">
            <span class="font-bold text-lg">Supported games for tracking :</span>
            <ul class="list-disc">
                <li v-for="element in LIST_OF_GAMES">
                    {{ element.name }}
                </li>
            </ul>
        </div>
        <div class="p-6 align-top">
            <a href="https://github.com/OriginalTomPouce/anaptracker" target="_blank" class="cursor-pointer text-green-400 hover:text-white hover:underline">Github page</a>
        </div>
    </div>
</template>

<script>

    import LIST_OF_GAMES from "../listofgames.js";

    export default {
        name: 'home',
        props: {
        },
        data: function (
        ) {
            return {
                roomid: '',
                LIST_OF_GAMES,
                error: 0
            }
        },

        methods: {
            loadRoom: function () {
                this.error = 0;
                var roomstr = this.roomid;
                var fake_args = roomstr.split('/');
                var method = 'room';
                var webhost = 'archipelago';
                var id = fake_args[fake_args.length - 1];

                if (fake_args.length > 1 && fake_args[fake_args.length - 2] == 'tracker')
                    method = 'tracker';
                if (fake_args.length > 2)
                    webhost = this.$parent.webhostValue(fake_args[fake_args.length - 3]).alias;



                if (id.length == 22)
                    this.$parent.route(method, webhost, id);
                else
                    this.error = 1;
            }

        },
        components: {
        }
    }
</script>
