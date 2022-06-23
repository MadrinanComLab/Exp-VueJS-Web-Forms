<template>
  <form>
        <label>E-mail:</label>
        <input type="email" required v-model="email"><!--/ v-model ALLOWS US TO SAVE THE USER INPUT TO A VARIABLE. WHAT v-model DOES IS CALLED 2-WAY DATA BINDING /-->
      
        <label>Password:</label>
        <input type="password" required v-model="password">
      
        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>

        <!--/ FIRST WAY OF USING v-model TO A CHECKBOX /-->
        <div class="terms">
            <input type="checkbox" required v-model="agreed">
            <label>Accept terms and conditions</label>
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

    <p>Email: {{ email }}</p>
    <p>Pasword: {{ password }}</p>
    <p>Role: {{ role }}</p>
    <p>Agrees to terms and conditions: {{ agreed }}</p>
    <!--/ <p>Names: {{ names }}</p> /-->
</template>

<script>
export default {
    data() {
        return {
            email: "name@example.com", // THIS WILL SET AS DEFAULT VALUE OF EMAIL INPUT FIELD
            password: "",
            role: "developer", // THIS WILL SET AS DEFAULT VALUE OF COMBO BOX (<select>) TO Web Developer
            agreed: false,
            names: [],
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
</style>