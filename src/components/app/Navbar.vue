<template>
    <nav class="navbar orange lighten-1">
        <div class="nav-wrapper">
            <div class="navbar-left">
                <a @click.prevent="$emit('click')">
                    <i class="material-icons black-text">dehaze</i>
                </a>
                <span class="black-text">{{date | date('datetime')}}</span>
            </div>

            <ul class="right">
                <li>
                    <a
                        class="dropdown-trigger black-text"
                        href="#"
                        data-target="dropdown"
                        ref="dropdown"
                    >
                        <div class="navbar-text hide-on-small-and-down">USER NAME</div>
                        <i class="material-icons right">arrow_drop_down</i>
                    </a>

                    <ul id='dropdown' class='dropdown-content'>
                        <li>
                            <router-link to="/profile" class="black-text">
                                <i class="material-icons">account_circle</i>
                                <div class="navbar-text hide-on-small-and-down">Профиль</div>
                            </router-link>
                        </li>
                        <li class="divider" tabindex="-1"></li>
                        <li>
                            <a href="#" @click.prevent="logout" class="black-text">
                                <i class="material-icons">assignment_return</i>
                                <div class="navbar-text hide-on-small-and-down">Выйти</div>
                            </a>
                        </li>
                    </ul>
                </li>
            </ul>
        </div>
    </nav>
</template>

<style>
    .navbar-text {
        display: inline-flex;
    }
</style>

<script>
    export default {
        data:() => ({
            date: new Date(),
            interval: null,
            dropdown: null,
        }),
        methods: {
          logout() {
              this.$router.push('/login?message=logout')
          }
        },
        mounted() {
            this.interval = setInterval(() => {
                this.date = new Date()
            }, 1000)
            // eslint-disable-next-line no-undef
            this.dropdown = M.Dropdown.init(this.$refs.dropdown, {
                constrainWidth: true
            })
        },
        beforeDestroy() {
            clearInterval(this.interval)
            if (this.dropdown && this.dropdown.destroy) {
                this.dropdown.destroy()
            }
        }

    }
</script>