<template>
    <form @submit.prevent="submit">
        <div class="mb-3">
            <label class="form-label">Email address</label>
            <input type="email" class="form-control" v-model="email">
        </div>
        <div class="mb-3">
            <label class="form-label">Password</label>
            <input type="password" class="form-control" v-model="password">
            <div v-if="errorMsg" class="text-danger">{{errorMsg}}</div>
        </div>
        <div class="mb-3">
            <label class="form-label">Roles: </label>
            <select class="form-select" v-model="role">
                <option value="web developer">Web Developer</option>
                <option value="web designer">Web Designer</option>
            </select>
        </div>
        <div class="mb-3">
            <label class="form-label">Skills</label>
            <input type="text" class="form-control" @keyup.alt="addSkill" v-model="skill">
        </div>
        <div v-for="skill in skills" :key="skill">
            <p>{{ skill }} <span class="text-danger" @click="deleteSkill(skill)">&#x2716;</span></p>
        </div>
        <div class="mb-3 form-check">
            <input type="checkbox" class="form-check-input" v-model="check">
            <label class="form-check-label">Term and Condition</label>
        </div>
        <div class="mb-3 center">
            <button class="btn btn-primary">Create Account</button>
        </div>
    </form>
    <p>{{email}}</p>
    <p>{{password}}</p>
    <p>{{role}}</p>
    <p>{{check}}</p>
    <p>{{skills}}</p>
</template>

<script>
export default {
    data(){
        return{
            email: "daniel@gmail.com",
            password: "",
            role:"web developer",
            check: false,
            skills: [],
            skill: "",
            errorMsg: ""
        }
    },
        methods:{
            addSkill(e){
                if(e.key==="," && this.skill){
                    this.skills.push(this.skill);
                    this.skill =""
                }
            },
            deleteSkill(skill){
                this.skills = this.skills.filter((loopSkill)=>{//skill ka click , looSkill ka all data in array
                    return loopSkill != skill; 
                })
            },
            submit(){
                if(this.password.length<8){
                    this.errorMsg="Password must be at least 8 character";
                }
            }
        }
}
</script>

<style scoped>
form{
    margin: 20px auto;
    background-color: white;
    max-width: 420px;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
.option-form{
    width: 100%;
    margin-top: 10px;
}
p {
color: #333;
}
</style>