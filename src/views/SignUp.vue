<template>
    <div>
        <div class="container">
            <form @submit="checkFromButton"
                  @input="validateForm">
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
                       v-bind:class="{'is-danger': loginError}"
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
                       v-bind:class="{ 'is-danger': phoneError}"
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
                       v-bind:class="{'is-danger': passwordError}"
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

                loginError: false,
                phoneError: false,
                passwordError: false,

                loginMessage: "",
                phoneMessage: "",
                passwordMessage: "",

                firstCheck: false,
            }),

        methods: {
            checkFormat: function (field) {

                let rawLength = field.length;
                let formattedLength = (field === this.phone)
                    ? field.replace(/[^0-9_]/g, "").length
                    : field.replace(/[^a-zA-Z0-9_]/g, "").length;

                if (!rawLength) {
                    return "Обязательное поле"
                } else if (rawLength === formattedLength) {
                    return "Недопустимые символы"
                }

                if (field === this.login && formattedLength < 5) {
                    return "Введите больше 5 символов";
                }

                if (field === this.phone && formattedLength !== 11) {
                    return "Введите 11 цифр";
                }

                if (field === this.password && formattedLength < 6) {
                    return "Введите больше 6 символов";
                }

                return "";
            },


            checkFromButton: function(event){
                this.firstCheck = true;
                event.preventDefault();

                if (this.validateForm(event)) {
                    alert("Yahoo!");
                } else {
                    event.preventDefault();
                }
            },

            validateForm: function (event) {
                event.preventDefault();

                if (!this.firstCheck) {
                    return;
                }

                this.loginMessage =  this.checkFormat(this.login);
                this.phoneMessage = this.checkFormat(this.phone);
                this.passwordMessage = this.checkFormat(this.password);

                this.loginError = Boolean(this.loginMessage);
                this.phoneError = Boolean(this.phoneMessage);
                this.passwordError = Boolean(this.passwordMessage);

                return this.loginError || this.phoneError || this.passwordError;
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
</style>
