<template>
    <form>
        <div>
            <h4 class="text-5xl  drop-shadow-lg text-center shadow-black mt-28 mb-16">Add Employee</h4>
        </div>
        <div class="flex flex-col gap-5">
            <div>
                <label>Firstname</label>
                <input type="text" v-model="addName"
                    class="block  w-full py-1 px-2 mb-1   border border-gray-200 rounded" required>
                <label>Lastname</label>
                <input type="text" v-model="addLastName"
                    class="block  w-full py-1 px-2 mb-1   border border-gray-200 rounded" required>
            </div>
            <div>
                <label>Email</label>
                <input type="email" v-model="addEmail"
                    class=" w-full py-1 px-2 mb-1 text-gray-800 border border-gray-200 rounded" required>
            </div>
            <div>
                <label>Username</label>
                <input type="text" v-model="addUsername"
                    class="block appearance-none w-full py-1 px-2 mb-1 text-base leading-normal bg-white text-gray-800 border border-gray-200 rounded"
                    required>
            </div>
            <div>
                <label>Phone</label>
                <input type="number" v-model="addPhone"
                    class=" w-full py-1 px-2 mb-1 text-base  bg-white text-gray-800 border border-gray-200 rounded"
                    required>
            </div>
        </div>
        <div class="flex justify-center gap-4 mt-2">
            <router-link to="/" class="mt-1">Cancel</router-link>
            <router-link :to="{ name: 'home' }" class=" text-center  py-1 px-3  bg-green-500 text-white hover:green-600"
                @click="add">Add
            </router-link>
        </div>
    </form>
</template>
<script>
export default {
    name: 'AddUser',
    data() {
        return {
            newUsers: [],
            addLastName: '',
            addName: '',
            addEmail: '',
            addUsername: '',
            addPhone: '',
        }
    },
    methods: {
        add() {
            const newrow = { image: "https://robohash.org/GDZ.png?set=set2", firstName: this.addName, lastName: this.addLastName, email: this.addEmail, username: this.addUsername, phone: this.addPhone };
            const user = JSON.parse(localStorage.getItem("userTable"));
            user.push(newrow);
            localStorage.setItem("userTable", JSON.stringify(user));
            fetch(`https://dummyjson.com/users/add`, {
                method: 'POST',
                body: JSON.stringify({
                    image: newrow.image,
                    firstName: newrow.firstName,
                    lastName: newrow.lastName,
                    email: newrow.email,
                    phone: newrow.phone
                }),
            }).then(res => {
                if (res.ok) {
                    console.log({
                        image: newrow.image,
                        firstName: newrow.firstName,
                        lastName: newrow.lastName,
                        email: newrow.email,
                        phone: newrow.phone
                    });
                }
            })
        }
    }
}
</script>
<style lang="scss" scoped>

</style>