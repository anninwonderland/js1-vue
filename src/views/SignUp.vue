<template>
    <div>
        <div class="container">
            <form>
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
                        >
                    </div>
                    <p class="help"
                       id="login-error"
                       v-model="loginError"
                       v-bind:class="{ hidden: isHidden }"
                    > {{errorMessage}}</p>
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
                        >
                    </div>
                    <p class="help"
                       id="phone-error"
                       v-model="phoneError"
                       v-bind:class="{ hidden: isHidden }"
                    >{{errorMessage}}</p>
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
                        >
                    </div>
                    <p class="help"
                       id="password-error"
                       v-model="passwordError"
                       v-bind:class="{ hidden: isHidden }"
                    >{{errorMessage}}</p>
                </div>
                <div class="control">
                    <button class="button"
                            type="submit"
                            @submit="checkForm"
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
                login: null,
                phone: null,
                password: null,

                loginError: null,
                phoneError: null,
                passwordError: null,

                isHidden: true,

                errorMessage: "Заполните поле",
            }),

        methods: {
            formatted: function(field) {
                let rawLength = field.length;
                let formattedLength = field.replace(/[^0-9]/g, "").length;

                return (rawLength === formattedLength);
            },

            checkForm: function(event) {

                let filled = (this.login && this.phone && this.password);
                let formatted = this.formatted(this.login) && this.formatted(this.phone) && this.formatted(this.password);

                console.log("login: " + this.login);
                console.log("formatted: " + formatted);
                console.log("filled: " + filled);

                if (filled && formatted) {
                    //no errors
                    console.log("filled && formatted");
                    return true;
                }

                if (!this.login) {
                    this.isHidden = false;
                }

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

    .hidden {
        visibility: hidden;
    }
</style>
