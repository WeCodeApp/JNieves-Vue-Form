<template>
    <div class="max-w-lg mx-auto p-6 bg-white rounded-lg shadow-md w-1/2">
        <form @submit.prevent="handleSubmit">
        <div class="mb-4">
            <label for="email" class="block text-sm font-medium text-gray-700"
            >Email</label
            >
            <input
            type="email"
            id="email"
            v-model="email"
            required
            class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
            />
        </div>
        <div class="mb-4">
            <label for="password" class="block text-sm font-medium text-gray-700"
            >Password</label
            >
            <input
            type="password"
            id="password"
            v-model="password"
            required
            class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
            />
        </div>

        <div class="mb-4">
            <label>Roles</label>
            <select
            class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
            >
            <option value="dev">Web Developer</option>
            <option value="design">Web Designer</option>
            </select>
        </div>

        <div class="p-4 bg-gray-100 rounded-lg shadow-md mb-4">
            <label>Names:</label>
            <div class="mb-2">
            <input type="checkbox" value="sam" v-model="names" id="sam">
            <label for="sam" class="text-sm text-gray-600"> Sam</label>
            </div>
            <div class="mb-2">
            <input type="checkbox" value="mae" v-model="names" id="mae">
            <label for="mae" class="text-sm text-gray-600"> Mae</label>
            </div>
            <div class="mb-2">
            <input type="checkbox" value="jai" v-model="names" id="jai">
            <label for="jai" class="text-sm text-gray-600"> Jai</label>
            </div>
        </div>

        <div>
            <label>Skills:</label>
            <input 
                type="text" 
                v-model="tempSkill" 
                @keydown.enter.prevent="addskill" 
                class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm" 
                placeholder="Add a skill (press Enter to add)"
            >
            <div v-for="skill in skills" :key="skill" class="bg-gray-200 p-2 m-1 rounded-md inline-block">
                {{ skill }}
            <button @click="removeSkill(skill)" class="ml-2 text-black">x</button>

            </div>
            <p v-if="skillError" class="text-red-500 text-sm">{{ skillError }}</p>
        </div>

        <div class="my-4">
            <input type="checkbox" v-model="acceptTerms" id="acceptTerms" required />
            <label for="acceptTerms" class="text-sm text-gray-600"> Accept Terms and Conditions</label> 
        </div>

        <button
            type="submit"
            class="w-full py-2 px-4 bg-blue-600 text-white font-semibold rounded-md shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
        >
            Create an Account
        </button>
    </form>

    <div class="mt-6 p-4 bg-gray-100 rounded-lg shadow-inner break-words">
        <p class="text-gray-700"><strong>Email:</strong> {{ email }}</p>
        <p class="text-gray-700"><strong>Password:</strong> {{ password }}</p>
        <p class="text-gray-700"><strong>Role:</strong> {{ role }}</p>
        <p class="text-gray-700"><strong>Accept Terms:</strong> {{ acceptTerms }}</p>
        <p class="text-gray-700"><strong>Names:</strong> {{ names }}</p>
    </div>
    </div>
</template>

<script>
export default {
    name: "SignupForm",
    data() {
        return {
        email: "",
        password: "",
        role: "dev",
        acceptTerms: false,
        names: [],
        skills: [],
        tempSkill: "",
        skillError: "",
        };
    },
    methods: {
        addskill() {
            let skill = this.tempSkill.trim();
            
            if (skill) {
                if (this.skills.includes(skill)) {
                    this.skillError = `"${skill}" is already in your skills list`;
                } else {
                    this.skills.push(skill);
                    this.skillError = "";
                }
            }
            this.tempSkill = "";
        },
        removeSkill(skill) {
            this.skills = this.skills.filter(item => item !== skill);
        },
        handleSubmit() {
            this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 5 characters long';

            if (!this.passwordError) {
            alert(`Form submitted with data:
                Email: ${this.email}
                Password: ${this.password}
                Role: ${this.role}
                Accept Terms: ${this.acceptTerms}
                Names: ${this.names.join(', ')}
                Skills: ${this.skills.join(', ')}`);
            }
        }
    }
};
</script>
