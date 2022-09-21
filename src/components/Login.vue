<template>

    <form @submit.prevent="onSubmit">

      <article class="container-form--title">
        <h3>Sign in</h3>
      </article>

      <article class="container-form--inputs">

        <label for="typeEmail">* Usuario</label>
        <input
          type="text"
          id="typeEmail"
          name="login"
          placeholder="Ingresá tu email"
          title="ej: juan.perez@dominio.extensión"
          v-model="username">
        <p v-show="wrongEmail" class="text-error">email incorrecto</p>

        <label for="typePassword">* Contraseña</label>
        <input
          type="password"
          id="typePassword"
          name="login"
          placeholder="Ingresá tu contraseña"
          v-model="password">
        <p v-show="wrongPassword" class="text-error">Contraseña incorrecta</p> 
       
      </article>

      <article class="container-form--password">

        <div>
          <label for="tickCheck">Recordar Contraseña</label>
          <input
            type="checkbox"
            name=""
            id="tickCheck"
            v-model="rememberPassword">
        </div>

        <div>
          <a href="#!">¿Olvidaste la Contraseña?</a>
        </div>

      </article>

      <article class="container-form--login">
        <button type="submit">Login</button>
        <p class="text-error"></p>
      </article>

    </form>

</template>

<script>

import axios from 'axios'
export default {
    data() {
        return {
            username: null,
            password: null,
            wrongEmail: false,
            wrongPassword: false,
            rememberPassword: false,
        }
    },

    methods: {
      
      onSubmit() {
        const emailRe =
          /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/

        if(emailRe.test(this.username)) {
          this.wrongEmail = false
        } else {
          this.wrongEmail = true
        }

        if(this.password) {
          this.wrongPassword = false
        } else {
          this.wrongPassword = true
        }

        let json = {
          'username': this.username,
          'password': this.password
        }

        console.log('user y pass submitted', json)
        axios.post('http://localhost:3000/login', json).then(data => {
          console.log(data)
        })

      }
    }
}
</script>

<style scoped>

form {
    display: flex;
    flex-direction: column;

    gap: 10px;
}

.container-form--inputs {
    display: flex;
    flex-direction: column;

    gap: 10px;
}

.container-form--password {
    display: flex;
    justify-content: space-evenly;
}

.container-form--login {
    display: flex;
    justify-content: center;
}

button {
    width: 150px;
    height: 50px;
}

.text-error {
  color: red;
}



</style>