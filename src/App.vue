<template>
    <div id="app">
        <div class="container">
            <InputGroup
                imageSrc="https://via.placeholder.com/60/ddd/808080"
                title="Hugh is"
                placeholder="7"
                afterText="hours old"
                v-model="value1"/>

            <InputGroup
                imageSrc="https://via.placeholder.com/60/aaa/404040"
                title="Charlotte is"
                placeholder="7"
                afterText="hours old"
                v-model="value2"/>

            <InputGroup
                imageSrc="https://via.placeholder.com/60/777/202020"
                title="Alexander is"
                placeholder="7"
                afterText="hours old"
                v-model="value3"/>
        </div>
    </div>
</template>

<script>
import InputGroup from '@/components/InputGroup';

export default {
    name: 'App',

    components: {
        InputGroup
    },

    data() {
        return {
            value1: '',
            value2: '',
            value3: '2500'
        };
    },

    watch: {
        value1() {
            console.log(`value1 is: ${this.value1}`);
        },
        value2() {
            console.log(`value2 is: ${this.value2}`);
        },
        value3() {
            console.log(`value3 is: ${this.value3}`);
        }
    }
};
</script>

<style lang="scss">
*,
*::before,
*::after{
    box-sizing: border-box;
}
html,
body{
    min-height: 100vh;
    font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Helvetica Neue,Arial,Noto Sans,sans-serif,Apple Color Emoji,Segoe UI Emoji,Segoe UI Symbol,Noto Color Emoji;
}
body{
    margin: 0;
}

#app{
    width: 100%;
    min-height: 100vh;
    padding: 10px 0 40px;
}

.container{
    max-width: 1366px;
    padding: 0 20px;
    margin: 0 auto;
}
</style>
