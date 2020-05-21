<template>
    <div id="app" class="bg-gray-600">
        <div class="min-h-screen w-screen pl-64 pt-20">
            <label class="text-gray-200 shadow font-semibold font-sans">Nuevo usuario</label>
            <input type="text" 
                v-model="newUserName"
                class="bg-white focus:outline-none focus:shadow-outline border border-gray-300 rounded-lg py-2 px-4 block appearance-none leading-normal mb-2"
                v-on:keyup.enter="addUser"
                placeholder="Presione ENTER para agregarlo"/>
            <Draggable v-if="users.length > 0" tag="ul" class="w-full max-w-md" :list="users" :animation="200">
                <li is="user-card" 
                    v-for="user in users" 
                    :user="user" 
                    :key="user.id"
                    v-on:delete-user="deleteUser">
                </li>
            </Draggable>
            <div v-else>
                <h2 class="text-gray-200 text-3xl">No hay usuarios registrados</h2>
            </div>
        </div>
    </div>
</template>

<script>

import Draggable from 'vuedraggable'
import UserCard from './components/UserCard.vue'

const avatars = [
    'https://pickaface.net/gallery/avatar/unr_sample_161118_2054_ynlrg.png',
    'https://pickaface.net/gallery/avatar/freud51c8b3f65e7dc.png',
    'https://pickaface.net/gallery/avatar/Opi51c74d0125fd4.png',
    'https://pickaface.net/gallery/avatar/unr_yassine_191124_2012_3gngr.png',
    'https://pickaface.net/gallery/avatar/elmedinilla541c03412955c.png'
];

export default {
    name: 'App',
    
    components: {
        Draggable,
        UserCard
    },

    data() {
        return {
            newUserName: '',
            nextID: 6, 
            users: [
                {
                    id: 1,
                    name: "Evan You",
                    avatar: avatars[0],
                },
                {
                    id: 2,
                    name: "Taylor Otwell",
                    avatar: avatars[1]
                },
                {
                    id: 3,
                    name: "Steve Jobs",
                    avatar: avatars[2]
                },
                {
                    id: 4,
                    name: "Linus Torvalds",
                    avatar: avatars[3]
                },
                {
                    id: 5,
                    name: "Bill Gates",
                    avatar: avatars[4]
                }
            ]
        }
    },

    methods: {
        addUser() {
            if (this.newUserName !== '') {
                let avatarIndex = Math.floor(Math.random() * (avatars.length));
    
                this.users.push({
                    id: this.nextID++,
                    name: this.newUserName,
                    avatar: avatars[avatarIndex]
                });
    
                this.newUserName = '';
            }
        },

        deleteUser(user) {
            var index = this.users.indexOf(user);
            this.users.splice(index, 1);
        }
    }
}
</script>

<style lang="scss">
    .moving-card {
        @apply opacity-50 bg-gray-100 border border-blue-500;
    }
</style>
