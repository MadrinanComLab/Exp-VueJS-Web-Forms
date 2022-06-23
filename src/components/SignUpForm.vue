<template>
  <!--/ BY DEFAULT, IF A SUBMIT BUTTON WAS CLICKED THE PAGE WILL BE REFRESH /-->
  <!--/ BUT USING @submit.prevent WILL PREVENT THIS DEFAULT ACTION /-->
  <!--/ .prevent IS JUST AN EVENT MODIFIER, YOU CAN USE @submit ONLY, BUT THAT WILL REFRESH THE PAGE ON SUBMISSION AS DEFAULT /-->
  <form @submit.prevent="handleSubmit">
        <label>E-mail:</label>
        <input type="email" required v-model="email"><!--/ v-model ALLOWS US TO SAVE THE USER INPUT TO A VARIABLE. WHAT v-model DOES IS CALLED 2-WAY DATA BINDING /-->
      
        <label>Password:</label>
        <input type="password" required v-model="password">
        <div v-show="passwordErr" class="error">{{ passwordErr }}</div>
      
        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup.alt="addSkill"><!--/ FUNCTION INSIDE @keyup.alt WILL FIRES WHEN ALT WAS PRESS PLUS THE CONDITION INSIDE THIS FUNCTION /-->

        <div v-for="skill in skills" :key="skill" class="pill">
            <span @click="removeSkill(skill)">{{ skill }}</span>
        </div>

        <!--/ FIRST WAY OF USING v-model TO A CHECKBOX /-->
        <div class="terms">
            <input type="checkbox" required v-model="agreed">
            <label>Accept terms and conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>

        <!--/ SECOND WAY OF USING v-model TO A CHECKBOX /-->
        <!--/ <div> v-model ALLOWS US TO SELECT MULTPLE VALUE BY STORING IT IN AN ARRAY
            <input type="checkbox" value="John" v-model="names">
            <label>John</label>

            <input type="checkbox" value="Melanie" v-model="names">
            <label>Melanie</label>
            
            <input type="checkbox" value="Chris" v-model="names">
            <label>Chris</label>
        </div> /-->
    </form>

    <!--/ <p>Email: {{ email }}</p>
    <p>Pasword: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Agrees to terms and conditions: {{ agreed }}</p>
    <p>Names: {{ names }}</p> /-->
</template>

<script>
export default {
    data() {
        return {
            email: "", // THIS WILL SET AS DEFAULT VALUE OF EMAIL INPUT FIELD
            password: "",
            role: "developer", // THIS WILL SET AS DEFAULT VALUE OF COMBO BOX (<select>) TO Web Developer
            agreed: false,
            names: [],
            tempSkill: "",
            skills: [],
            passwordErr: ""
        }
    },

    methods: {
        addSkill(e) {
            if (e.key === "," && this.tempSkill)
            {
                if (!this.skills.includes(this.tempSkill)) // .replace(",", "")
                {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ""
            }
        },

        removeSkill(skill) {
            // THIS IS A QUICK WAY OF REMOVING ITEM IN AN ARRAY.
            // IF YOU WANT TO KNOW MORE ABOUT FILTER FUNCTION OF AN ARRAY, HERE IS THE LINK:
            // https://www.w3schools.com/jsref/jsref_filter.asp
            
            this.skills = this.skills.filter((item) => {
                return skill !== item
            })
        },

        handleSubmit() {
            this.passwordErr = this.password.length > 5 ? "" : "Password must be at least 6 characters long"

            if (!this.passwordErr)
            {
                console.log("Email: " + this.email)
                console.log("Password: " + this.password)
                console.log("Role: " + this.role)
                console.log("Skills: " + this.skills)
                console.log("Terms Accepted: " + this.agreed)
            }
        }
    }
}
</script>

<style>
    form {
        max-width: 420px;
        margin: 30px auto;
        background: #FFF;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }

    label {
        color: #AAA;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }

    input, select {
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: solid 1px #DDD;
        color: #555;
    }

    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }

    .pill {
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #EEE;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }

    button {
        background: #0B6DFF;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: #FFF;
        border-radius: 20px;
    }

    .submit {
        text-align: center;
    }

    .error {
        color: #FF0062;
        margin-top: 10px;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>