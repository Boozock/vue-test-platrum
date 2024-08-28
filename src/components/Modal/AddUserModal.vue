<template>
    <div class="modal-wrpr" @click.self.stop="close">
        <div class="modal">
            <div class="modal-header">
                <h3 class="modal-title">Добавление пользователя</h3>
                <a href="#" class="close-modal" @click.prevent="close">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M3 3L12.5 12.5M12.5 12.5L22 3M12.5 12.5L3 22M12.5 12.5L22 22" stroke="white" stroke-width="3" stroke-linecap="round"/>
                    </svg>
                </a>
            </div>
            <div class="modal-body">
                <div class="form-group">
                    <label class="form-label">Имя</label>
                    <input type="text" class="input-text" v-model="newUser.name">
                </div>
                <div class="form-group">
                    <label class="form-label">Телефон</label>
                    <input type="tel" class="input-text" v-model="newUser.phone">
                </div>
                <div class="form-group" v-if="users.length">
                    <label class="form-label">Начальник</label>
                    <select name="" id="" class="select" v-model="newUser.boss">
                        <option value="" hidden></option>
                        <option v-for="user in users" :key="user.id" :value="user.id">
                            {{ user.name }}
                        </option>
                    </select>
                </div>
                <Button
                    title="Сохранить"
                    :click="addUser"
                    :disabled="!newUser.name.length || !newUser.phone.length"
                />
            </div>
        </div>
    </div>
</template>

<script>
import Button from '@/components/Base/Button';
import uniqid from 'uniqid';

export default {
    name: "AddUserModal",
    components: {
        Button,
    },
    props: ["close", "users", "add"],
    data(){
        return {
            newUser: {
                name: "",
                phone: "",
                boss: "",
                id: uniqid(),
            }

        }
    },
    // computed: {
    //     filteredUsers(){
    //         return this.users.filter(item => !item.boss);
    //     }
    // },
    methods: {
        addUser(){
            if(this.newUser.name && this.newUser.phone){        
                this.add(this.newUser);
            }
        }
    }
}
</script>