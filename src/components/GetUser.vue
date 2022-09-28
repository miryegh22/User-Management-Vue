<template>
    <tr v-for="r,index in root">
        <td>
            {{index+1}}
        </td>
        <td>
            <img :src="r.image" class="w-20" alt="">
        </td>
        <td>{{r.firstName +" " + r.lastName}}</td>
        <td>{{r.email}}</td>
        <td>{{r.username}}</td>
        <td>{{r.phone}}</td>
        <td>
            <button class="delete" data-toggle="modal"><svg xmlns="http://www.w3.org/2000/svg"
                    @click="deleteUser(index)" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor"
                    class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="M20.25 7.5l-.625 10.632a2.25 2.25 0 01-2.247 2.118H6.622a2.25 2.25 0 01-2.247-2.118L3.75 7.5m6 4.125l2.25 2.25m0 0l2.25 2.25M12 13.875l2.25-2.25M12 13.875l-2.25 2.25M3.375 7.5h17.25c.621 0 1.125-.504 1.125-1.125v-1.5c0-.621-.504-1.125-1.125-1.125H3.375c-.621 0-1.125.504-1.125 1.125v1.5c0 .621.504 1.125 1.125 1.125z" />
                </svg>
            </button>
        </td>
    </tr>
</template>
<script>
export default {
    name: "GetUser",
    methods: {
        deleteUser(index) {
            fetch(`https://dummyjson.com/users/${index + 1}`, {
                method: 'DELETE',
            }).then(res => {
                if (res.ok) {
                    this.root.splice(index, 1);
                    localStorage.setItem("userTable", JSON.stringify(this.root));
                }
            })
        }
    },
    data() {
        return {
            data: ''
        }
    },
    props: {
        root: {},
    },
}
</script>
<style lang="scss" scoped>

</style>