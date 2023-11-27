<template>
    <form @submit="handleSubmit">
        <h3>Create your account!</h3>
        <label>Email:</label>
        <input required type="email" v-model="email" />

        <label>Password:</label>
        <input required type="password" v-model="password" />
        <div v-if="passwordError !== ''" class="error">{{ passwordError }}</div>

        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Experience:</label>
        <select v-model="exp">
            <option value="junior">Junior</option>
            <option value="semisenior">Semi-Senior</option>
            <option value="senior">Senior</option>
        </select>

        <label>Skills:</label>
        <div class="skills-input-container">
            <input type="text" v-model="tempSkill"/> 
            <span class="material-symbols-rounded" @click="addSkill">add</span>
        </div>

        <div class="pill-container">
            <div v-for="skill in skills" :key="skill" class="pill">
                {{ skill }}
                <span class="material-symbols-rounded" @click="deleteSkill(skill)">delete</span>
            </div>
        </div>

        <div class="terms">
            <input type="checkbox" required v-model="terms">
            <label>I agree to the terms and conditions</label>
        </div>
        <div class="submit">
            <button type="submit">Create Account</button>
        </div>
    </form>
</template>

<script setup>
import { ref } from 'vue';

const email = ref('');
const password = ref('');
const role = ref('');
const terms = ref(false);
const exp = ref('');
const tempSkill = ref('');
const skills = ref([]);
const passwordError = ref('');

const props = defineProps({
    onSubmit: {
        type: Function,
    }
})

const addSkill = (e) => {
    if(tempSkill.value.trim() !== '' && tempSkill.value !== null){

        if(!skills.value.includes(tempSkill.value)){
            skills.value.push(tempSkill.value);            
        }
        tempSkill.value = '';
    }
}

const deleteSkill = (skill) => {
    const index = skills.value.indexOf(skill);
    if (index !== -1) {
        skills.value.splice(index, 1);
    }
}

const handleSubmit = (e) => {
    e.preventDefault();
    passwordError.value = password.value.length < 8 ? 'Password must be at least 6 characters long' : '';
    
    if(passwordError.value === ''){
        props.onSubmit({
            email: email.value,
            password: password.value,
            role: role.value,
            exp: exp.value,
            skills: skills.value,
        });
    }
}


</script>

<style>
h3{
    text-align: center;
    font-weight: 500;
    font-size: 25px;
    margin: 0px 0px 0px 0px;
}
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 1px;
}

input, select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

select{
    border-radius: 4px;
    cursor: pointer;
}

input[type="checkbox"]{
    cursor: pointer;
    display: inline-block;
    width: 16px;
    margin: 0 10px 0 0;
    position: relative;
    top: 2px;
}

.pill-container {
    display: flex;
    flex-wrap: wrap;
    margin-top: 20px;
}

.pill{
    text-transform: capitalize;
    margin: 5px;
    padding: 6px 12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: 500;
    color: #777;  
    display: flex;
    align-items: center;
    width: fit-content;
    user-select: none;
}

.pill .material-symbols-rounded:hover{
    color:red;
}

.material-symbols-rounded{
    transform: scale(0.8);
    cursor: pointer;
}

button{
    background: #0b6dff;
    border: none;
    padding: 10px 20px;
    color: white;
    border-radius: 20px;
    font-weight: 500;
    cursor: pointer;
    transition: background 0.1s;
}

button:hover{
    background: #0a5cd1;
}

.submit{
    margin-top: 10px;
    text-align: center;
}

.error {
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8rem;
    font-weight: 500;
}

.skills-input-container {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
}

.skills-input-container input {
    flex: 1;
    margin-right: 5px;
}

.skills-input-container .material-symbols-rounded{
    transition: all 0.03s ease-in;
}

.skills-input-container .material-symbols-rounded:hover{
    transform: scale(1.2);
}
</style>