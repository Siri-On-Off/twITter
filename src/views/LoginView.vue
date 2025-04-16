<script setup>
import { ref } from 'vue';
import { loginUser } from '../api/requests.js';
import { useRouter } from 'vue-router';

const email = ref('');
const password = ref('');
const errors = ref({});
const router = useRouter();

async function login() {
  try {
    // Versuche, den Benutzer einzuloggen.
    await loginUser(email.value, password.value);
    // Alles okay! Umleiten zur HomeView
    await router.push('/')
  } catch (exception) {
    // Die Zugangsdaten waren falsch, logge die Exception.
    console.error("login error", exception);

    // Übernehme die Fehlermeldungen aus der Exception. 
    errors.value = exception.errors;
  }
}
</script>

<template>
  <div class="login">
    <section class="login-wrapper">
      <form action="#" class="login-form" @submit.prevent="login">
        <div class="form-group">
          <label class="form-label" for="email">E-Mail</label>
          <input class="form-input" type="email" id="email" v-model="email" />
          <div class="form-error" v-if="errors.email">
            {{ errors.email }}
          </div>
        </div>
        <div class="form-group">
          <label class="form-label" for="password">Passwort</label>
          <input
            class="form-input"
            type="password"
            id="password"
            v-model="password"
          />
          <div class="form-error" v-if="errors.password">
            {{ errors.password }}
          </div>
        </div>
        <div class="form-group">
          <button
            :disabled="email.length === 0 || password.length === 0"
            class="btn btn--primary btn--block"
          >
            Login
          </button>
        </div>
      </form>
    </section>
  </div>
</template>