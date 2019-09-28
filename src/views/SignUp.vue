<template>
    <div>
        <div class="container">
            <form @submit.once="checkForm"
                  @input="checkForm">
                <div class="field">
                    <label for="login"
                           class="label"
                    >Логин</label>
                    <div class="control">
                        <input class="input"
                               type="text"
                               name="login"
                               id="login"
                               v-model="login"
                               v-bind:class="{'is-danger': loginError}"
                        >
                    </div>
                    <p class="help"
                       id="login-error"
                       v-bind:class="{'is-hidden': !loginError,
                                      'is-danger': loginError}"
                    > {{loginMessage}}</p>
                </div>
                <div class="field">
                    <label for="phone"
                           class="label"
                    >Телефон</label>
                    <div class="control">
                        <input class="input"
                               type="tel" name="phone"
                               id="phone"
                               v-model="phone"
                               v-bind:class="{'is-danger': phoneError}"
                        >
                    </div>
                    <p class="help"
                       id="phone-error"
                       v-model="phoneError"
                       v-bind:class="{'is-hidden': !phoneError,
                                      'is-danger': phoneError}"
                    >{{phoneMessage}}</p>
                </div>
                <div class="field">
                    <label for="password"
                           class="label"
                    >Пароль</label>
                    <div class="control">
                        <input class="input"
                               type="password"
                               name="password"
                               id="password"
                               v-model="password"
                               v-bind:class="{'is-danger': passwordError}"
                        >
                    </div>
                    <p class="help"
                       id="password-error"
                       v-model="passwordError"
                       v-bind:class="{'is-hidden': !passwordError,
                                      'is-danger': passwordError}"
                    >{{passwordMessage}}</p>
                </div>
                <div class="control">
                    <button class="button"
                            type="submit"
                            @click="firstCheck = true"
                    >Войти
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'signUp',
        data: () => (
            {
                login: "",
                phone: "",
                password: "",

                loginError: false,
                phoneError: false,
                passwordError: false,

                loginMessage: "",
                phoneMessage: "",
                passwordMessage: "",

                firstCheck: false,
            }),

        methods: {
            formatted: function (field) {
                let rawLength = field.length;
                let formattedLength = field.replace(/[^a-zA-Z0-9_]/g, "").length;
                return (rawLength === formattedLength);
            },

            catchError: function (field) {
                if (!field) {
                    return "Заполните поле"
                } else if (!this.formatted(field)) {
                    return "Неверный формат";
                }
            },

            checkForm: function (event) {

                console.log(this.firstCheck);
                if (!this.firstCheck) {
                    return;
                }

                let filled = (this.login && this.phone && this.password);
                let formatted = this.formatted(this.login) && this.formatted(this.phone) && this.formatted(this.password);

                if (filled && formatted) {
                    alert("You're in!");
                    return true;
                }

                let res = this.catchError(this.login);

                if (res) {
                    this.loginMessage = res;
                    this.loginError = true;
                } else {
                    this.loginError = false;
                }

                res = this.catchError(this.phone);
                if (res) {
                    this.phoneMessage = res;
                    this.phoneError = true;
                } else {
                    this.phoneError = false;
                }

                res = this.catchError(this.password);
                if (res) {
                    this.passwordMessage = res;
                    this.passwordError = true;
                } else {
                    this.passwordError = false;
                }

                event.preventDefault();
            },
        },

    }
</script>

<style>
    body {
        margin: 0;
        padding: 0;

        font-family: Helvetica, serif;
        font-size: 14px;
    }

    .container {
        display: flex;
        padding-top: 10%;
        justify-content: center;
        width: 100%;
        height: 100%;
    }

    form {
        width: 20%;
    }

    .is-hidden {
        visibility: hidden;
    }
</style>
