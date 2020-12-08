<template>
    <form class="card auth-card" @submit.prevent="submitHendler">
        <div class="card-content">
            <span class="card-title">Домашняя бухгалтерия</span>
            <div class="input-field">
                <input
                        id="email"
                        type="text"
                        v-model="email"
                        :class="{invalid: ($v.email.$dirty && !$v.email.required) || ($v.email.$dirty && !$v.email.email)}"
                >
                <label for="email">Email</label>
                <small class="helper-text invalid" v-if="($v.email.$dirty && !$v.email.required)">Пусто, как в твоей голове, с***!!!!</small>
                <small class="helper-text invalid" v-else-if="($v.email.$dirty && !$v.email.email)">Ей с*** мыло напиши!!!!</small>
            </div>
            <div class="input-field">
                <input
                        id="password"
                        type="password"
                        v-model.trim="password"
                        :class="{invalid: ($v.password.$dirty && !$v.password.required) || ($v.password.$dirty && !$v.password.minLength)}"
                >
                <label for="password">Пароль</label>
                <small class="helper-text invalid" v-if="($v.password.$dirty && !$v.password.required)">И пароль от карточки пиши, а то п**да. Не пущу !!!!</small>
                <small class="helper-text invalid" v-if="($v.password.$dirty && !$v.password.minLength)">Не н**б*шь в пароле от карточки 4
                     цыферки !!!!</small>
            </div>
        </div>
        <div class="card-action">
            <div>
                <button
                        class="btn waves-effect waves-light auth-submit"
                        type="submit"
                >
                    Войти
                    <i class="material-icons right">send</i>
                </button>
            </div>

            <p class="center">
                Нет аккаунта?
                <router-link to="/register">Зарегистрироваться</router-link>
            </p>
        </div>
    </form>
</template>

<style>
    @media screen and (max-width: 576px) {
        .auth-card {
            width: 320px;
        }
    }
</style>


<script>
    import {email, required, minLength} from 'vuelidate/lib/validators'
    export default {
        name: 'login',
        data: () => ({
            email: '',
            password: '',
        }),
        validations: {
            email: {email, required},
            password: {required, minLength: minLength(4)}
        },
        methods: {
            submitHendler() {
                if (this.$v.$invalid) {
                    this.$v.$touch()
                    return
                }
                const formDate = {
                    email: this.email,
                    password: this.password
                }
                console.log("Спасибо за номер карточки друг" + formDate)
                this.$router.push('/')
            }
        }
    }
</script>