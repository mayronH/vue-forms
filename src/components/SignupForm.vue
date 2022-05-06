<template>
  <form class="form" @submit.prevent="handleForm" @keypress.enter.prevent>
    <fieldset>
      <label for="email_input">Email:</label>
      <input type="email" v-model="email" id="email_input" required />
    </fieldset>

    <fieldset>
      <label for="password_input">Password:</label>
      <input type="password" v-model="password" id="password_input" required />
      <div class="error-message" v-show="passwordError">
        {{ passwordError }}
      </div>
    </fieldset>

    <fieldset>
      <label for="role_input">Role:</label>
      <select name="role" id="role_input" v-model="role" required>
        <option value="" disabled>Select a Role</option>
        <option value="developer">Developer</option>
        <option value="webdesigner">Web Designer</option>
      </select>
    </fieldset>

    <fieldset>
      <label for="skill_input">Skills:</label>
      <input
        type="text"
        v-model="tempSkill"
        id="skill_input"
        placeholder="Press Enter to register a skill"
        @keydown.enter="addSkill"
      />

      <ul>
        <li v-for="skill in skills" :key="skill">
          {{ skill }}
          <button
            @click="removeSkill(skill)"
            role="delete"
            aria-label="delete skill"
            type="button"
          >
            x
          </button>
        </li>
      </ul>
    </fieldset>

    <fieldset class="terms">
      <input type="checkbox" id="checkbox_input" v-model="terms" required />
      <label for="checkbox_input"
        >Accept Terms and bind your <em>soul</em> to this company</label
      >
    </fieldset>

    <div class="button">
      <button class="submit-button">create an account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill() {
      if (this.tempSkill) {
        this.skills.push(this.tempSkill.toLowerCase());
        this.skills = [...new Set(this.skills)];

        this.tempSkill = "";
      }
    },
    removeSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill != item;
      });
    },
    handleForm() {
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 5 characters long";
    },
  },
};
</script>

<style>
.form {
  padding: 25px;

  background-color: var(--form-background);

  border-radius: 5px;
  border-bottom: 2px solid var(--accent);

  max-width: 520px;

  box-shadow: 5px 5px 5px 0px var(--shadow);
}
.terms {
  margin-top: 2rem;

  display: flex;
  align-items: center;
}
.terms em {
  color: var(--accent);
  font-weight: 600;
  font-style: normal;
  text-transform: uppercase;
}
.terms label,
.terms input {
  display: inline-block;
}
.terms input {
  border: 1px solid var(--accent);

  width: 1rem;

  margin: 0 1rem 0 0;
}

.form ul {
  margin: 0 0 0 24px;
  padding: 0;

  display: grid;
  gap: 1rem;
}

.form li {
  font-size: 1.1rem;
  text-transform: capitalize;

  padding-left: 0.5rem;
}

.form li::marker {
  content: "📑";
  font-size: 1.1em;
}

.form li button {
  cursor: pointer;

  border-radius: 50%;
  border: none;

  background-color: var(--accent);
  color: #fff;
  font-size: 0.5rem;

  width: 1rem;
  height: 1rem;

  margin-left: 0.5rem;

  transform: translate(0, -25%);
}

.button {
  display: flex;
  justify-content: center;

  margin-top: 1rem;
}

.submit-button {
  padding: 0.75rem 1.2rem;

  background-color: var(--accent);

  border-radius: 25px;
  border: none;

  color: #fff;
  font-size: 1rem;
  font-family: "Poppins Sans", sans-serif;
  text-align: center;

  transition: all 0.2s;
}

.submit-button:hover {
  transform: scale(1.1);
}

.error-message {
  color: #b91717;
  font-family: "Poppins Sans", sans-serif;
  font-size: 0.8rem;
  font-weight: 600;
  text-align: center;
  text-transform: lowercase;

  margin: 0.5rem 0;
}

@media (max-width: 520px) {
  .form {
    width: 100%;

    margin: 0px 25px;
  }
}
@media (max-width: 425px) {
  .terms input {
    width: 2rem;
  }
}
</style>