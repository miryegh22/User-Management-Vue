<template>
    <form>
        <div>
            <h4 class="text-5xl  drop-shadow-lg text-center shadow-black mt-28 mb-16">Add Employee</h4>
        </div>
        <div class="flex flex-col gap-5">
            <div>
                <label>Firstname</label>
                <input type="text" v-model="addName"
                    class="  w-full py-1 px-2 mb-1 text-green-800  border border-gray-200 rounded" required>
                <label>Lastname</label>
                <input type="text" v-model="addLastName"
                    class="block  w-full py-1 px-2 mb-1 text-green-800  border border-gray-200 rounded" required>
            </div>
            <div>
                <label>Email</label>
                <input type="email" v-bind:value="addEmail" @input="Email"
                    class=" w-full py-1 px-2 mb-1 text-gray-800 border border-gray-200 rounded"  required>
                  
            </div>
            <div>
                <label>Username</label>
                <input type="text" v-model="addUsername"
                    class="block  text-green-800 appearance-none w-full py-1 px-2 mb-1 text-base leading-normal bg-white text-gray-800 border border-gray-200 rounded"
                    required>
            </div>
            <div>
                <label>Phone</label>
                <div class="flex">
                <span>+</span>
                <input type="text" class=" w-full py-1 px-2 mb-1 text-base  bg-white text-gray-800 border border-gray-200 rounded" oninput="this.value = this.value.replace(/[^0-9.]/g, '').replace(/(\..*?)\..*/g, '$1');"   pattern="\d*"  minlength="12" maxlength="12"  v-bind:value="addPhone" @input="Phone"  placeholder="1234 1234 1234 " required>
               
                </div>
            </div>
        </div>
        <div class="flex justify-center gap-4 mt-2">
            <router-link to="/" class="mt-1">Cancel</router-link>
            <router-link :to="{ name: 'home' }" class=" text-center  py-1 px-3  bg-green-500 text-white hover:green-600"
                @click="add" >Add
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
            msg:''
           
        }
    },
    
    methods: {
        Email(event){
            this.addEmail=event.target.value;
            const reg=/^([a-zA-Z0-9/._]+)@([a-zA-Z0-9])+.([a-z]+)(.[a-z]+)?$/;
            if(reg.test(this.addEmail)){
                event.target.style.color="green"
            }
            else{
                event.target.style.color="red"
            }
        },
        Phone(event){
            this.addPhone=event.target.value;
            if(this.addPhone.length<12){
                event.target.style.color="red"}
            else{
                event.target.style.color="green"
            }
        },
         add() {
            const reg=/^([a-zA-Z0-9/._]+)@([a-zA-Z0-9])+.([a-z]+)(.[a-z]+)?$/;
            if(this.addName.length!=0 && this.addLastName.length!=0 && reg.test(this.addEmail) && this.addUsername.length!=0 && this.addPhone.length===12){
            const newrow = { image: "https://robohash.org/GDZ.png?set=set2", firstName: this.addName, lastName: this.addLastName, email: this.addEmail, username: this.addUsername, phone:'+'+ this.addPhone };
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
        
    }}}
}
</script>
<style lang="scss" scoped>

</style>
