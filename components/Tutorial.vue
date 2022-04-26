<template>
<fragment>
<div class="header-mode">
    <div class="mode-dark">
        <button @click="darkMode" name="mode" class="btn-mode ">
            <span>
                <svg v-show="light" xmlns="http://www.w3.org/2000/svg" width="45" height="45" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-sun darkMode-light" id="darkMode-light">
                    <circle cx="12" cy="12" r="5"></circle>
                    <line x1="12" y1="1" x2="12" y2="3"></line>
                    <line x1="12" y1="21" x2="12" y2="23"></line>
                    <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
                    <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
                    <line x1="1" y1="12" x2="3" y2="12"></line>
                    <line x1="21" y1="12" x2="23" y2="12"></line>
                    <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
                    <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
                </svg>
                <svg v-show="dark" xmlns="http://www.w3.org/2000/svg" width="45" height="45" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-moon darkMode-dark" id="darkMode-dark">
                    <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
                </svg>
            </span>
        </button>
    </div>
</div>
</fragment>
</template>

<script>
export default {
    name: 'darkMode',
    data() {
        return {
            light: true,
            dark: false
        }
    },
    methods: {
        darkMode() {
            this.light = !this.light
            this.dark = !this.dark
            console.log(this.light)
        }
    },
    mounted() {
        if (localStorage.getItem('darkMode') == 'enabled') {
            this.dark = true
            this.light = false
        } else {
            this.dark = false
            this.light = true
        }
    },
    watch: {
        dark: function (newVal, oldVal) {
            if (newVal) {
                localStorage.setItem('darkMode', 'enabled')
                document.body.classList.add('darkMode')

            } else {
                localStorage.setItem('darkMode', 'disabled')
                document.body.classList.remove('darkMode')
                document.body.classList.add('darkMode-off')
            }
        },
        light: function (newVal, oldVal) {
            if (newVal) {
                localStorage.setItem('darkMode', 'disabled')
                document.body.classList.remove('darkMode')
            } else {
                localStorage.setItem('darkMode', 'enabled')
                document.body.classList.add('darkMode')
                document.body.classList.remove('darkMode-off')
            }
        }
    }
}
</script>

<style>
body {
    background: #fafafa;
    color: black;
    padding: 0;
    margin: 0;
    font-family: 'Roboto', sans-serif;

}

.feather {
    color: #ff9100;
    height: 45px;
    width: 45px;
    padding: 5px;
    box-sizing: border-box;

}

body.darkMode {
    background: #212121;
    color: white;

}

.darkMode .feather {
    color: #0000ff;
    transform: translateY(90%);
}

.mode-dark {
    border: solid 2px #ff9100;
    width: 50px;
    height: 90px;
    border-radius: 20%;
}

.darkMode .mode-dark {
    border: solid 2px #0000ff;

}
</style>
