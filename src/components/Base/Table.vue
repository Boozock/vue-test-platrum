<template>
    <table class="table">
        <thead>
            <tr>
                <th @click="changeSort('name')" :class="{'active':sortBy === 'name'}">Имя</th>
                <th @click="changeSort('phone')" :class="{'active':sortBy === 'phone'}">Телефон</th>
            </tr>
        </thead>
        <tbody>
            <template v-for="user in sortUsers">
                <tr :key="user.id" v-if="!user.boss">
                    <td>{{ user.name }}</td>
                    <td>{{ user.phone }}</td>
                </tr>
                <tr v-for="userChild in users.filter(item => item.boss === user.id)" :key="userChild.id">
                    <td class="child-td">+ {{ userChild.name }}</td>
                    <td>{{ userChild.phone }}</td>
                </tr>
            </template>
        </tbody>
    </table>
</template>

<script>
export default {
    name: "Table",
    props: ["users"],
    data () {
        return {
            sortBy: null,
        }
    },
    computed:{
        sortUsers(){
            if(this.sortBy){
                return [...this.users].sort((a,b) => (a[this.sortBy] > b[this.sortBy]) ? 1 : ((b[this.sortBy] > a[this.sortBy]) ? -1 : 0));
            } else {
                return this.users;
            }
        }
    },
    methods:{
        changeSort(value){
            this.sortBy !== value ? this.sortBy = value : this.sortBy = null; 
        }
    },
}
</script>