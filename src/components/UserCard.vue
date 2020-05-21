<template>
    <transition name="bounce">
        <div class="p-4 mb-3 flex justify-between items-center bg-white shadow rounded-lg cursor-move">
            <div class="flex items-center">
                <img class="w-10 h-10 rounded-full" :src="user.avatar" :alt="user.name">
                <p v-show="!editing" class="ml-2 text-gray-700 font-semibold font-sans tracking-wide">{{user.name}}</p>
                <input v-show="editing" v-model="user.name" v-on:keyup.enter="toggleEditing" class="ml-2 px-2 py-1 border text-gray-700 font-semibold font-sans tracking-wide" />
            </div>
            <div class="flex">
                <button aria-label="Edit user" title="Editar usuario"
                        class="p-1 focus:outline-none focus:shadow-outline text-teal-500 hover:text-teal-600"
                        @click="onEdit">
                    <Edit3Icon/>
                </button>
                <button aria-label="Delete user" title="Eliminar usuario"
                        class="p-1 focus:outline-none focus:shadow-outline text-red-500 hover:text-red-600"
                        @click="onDelete">
                    <TrashIcon/>
                </button>
            </div>
        </div>
    </transition>
</template>

<script>
import { Edit3Icon, TrashIcon } from "vue-feather-icons";

export default {
    name: 'Card',

    components: {
        Edit3Icon,
        TrashIcon
    },

    props: {
        user: Object
    },

    data() {
        return {
            editing: false,
        }
    },
    
    methods: {
        onEdit() {
           this.toggleEditing();
        },
        
        onDelete() {
            this.$emit('delete-user', this.user);
        },

        toggleEditing() {
            this.editing = !this.editing;
        }
    }
}
</script>

<style lang="scss">
    .bounce-enter-active {
        animation: bounce-in .5s;
    }
    .bounce-leave-active {
        animation: bounce-in .5s reverse;
    }
    @keyframes bounce-in {
        0% {
            transform: scale(0);
        }
        50% {
            transform: scale(1.5);
        }
        100% {
            transform: scale(1);
        }
    }
</style>
