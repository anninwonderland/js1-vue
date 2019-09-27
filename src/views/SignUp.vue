<template>
    <div>
        <div class="container">
            <form @submit="checkForm">
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
                               v-bind:class="{'is-danger': ifError}"
                        >
                    </div>
                    <p class="help"
                       id="login-error"
                       v-bind:class="{'is-hidden': ifError,
                                      'is-danger': ifError}"
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
                               v-bind:class="{'is-danger': ifError}"
                        >
                    </div>
                    <p class="help"
                       id="phone-error"
                       v-model="phoneError"
                       v-bind:class="{'is-hidden': ifError,
                                      'is-danger': ifError}"
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
                               v-bind:class="{'is-danger': ifError}"
                        >
                    </div>
                    <p class="help"
                       id="password-error"
                       v-model="passwordError"
                       v-bind:class="{'is-hidden': ifError,
                                      'is-danger': ifError}"
                    >{{passwordMessage}}</p>
                </div>
                <div class="control">
                    <button class="button"
                            type="submit"
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

                loginError: null,
                phoneError: null,
                passwordError: null,

                ifError: true,

                loginMessage: "Заполните поле",
                phoneMessage: "Заполните поле",
                passwordMessage: "Заполните поле",
            }),

        methods: {
            formatted: function (field) {
                let rawLength = field.length;
                let formattedLength = field.replace(/[^a-zA-Z0-9_]/g, "").length;
                return (rawLength === formattedLength);
            },

            catchError: function (field, msg) {
                if (!field) {
                    msg = "Заполните поле";
                    this.ifError = false;
                } else if (!this.formatted(field)) {
                    msg = "Неверный формат";
                    this.ifError = false;
                } else {
                    this.ifError = true;
                }
            },

            checkForm: function (event) {
                let filled = (this.login && this.phone && this.password);
                let formatted = this.formatted(this.login) && this.formatted(this.phone) && this.formatted(this.password);

                if (filled && formatted) {
                    //no errors, do smth
                    console.log("filled && formatted");
                    return true;
                }

                this.catchError(this.login, this.loginMessage);
                console.log("is hidden: " + this.ifError);
                this.catchError(this.phone, this.phoneMessage);
                this.catchError(this.password, this.passwordMessage);

                event.preventDefault();
                console.log("PREVENTED");
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
