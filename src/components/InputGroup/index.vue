<template>
    <label class="input-group" :class="{'-focused': focused}">
        <div class="input-group__picture">
            <img
                class="input-group__image"
                :src="imageSrc"
                :alt="title"
                v-if="imageSrc">
        </div>

        <div class="input-group__content">
            <div class="input-group__title" v-if="title">{{title}}</div>
            <div class="input-group__width" ref="widthInput" aria-hidden="true">{{stateValue}}</div>
            <input
                class="input-group__input"
                type="text"
                v-model="stateValue"
                :placeholder="placeholder"
                :style="{width: inputWidth}"
                @focus="focus"
                @blur="blur">
            <div class="input-group__after-text" v-if="afterText">{{afterText}}</div>
        </div>
    </label>
</template>

<script>
const minWidth = 50;

export default {
    name: 'InputGroup',

    props: {
        imageSrc: {
            type: String,
            default: ''
        },
        title: {
            type: String,
            default: ''
        },
        afterText: {
            type: String,
            default: ''
        },

        value: {
            type: String,
            default: ''
        },
        placeholder: {
            type: String,
            default: ''
        },
    },

    data() {
        return {
            stateValue: '',
            focused: false,
            inputWidth: `${minWidth}px`
        };
    },

    watch: {
        value() {
            this.stateValue = this.value;
        },
        stateValue() {
            let stateValue = this.stateValue;
            //Удаляем все не-числовые символы
            if (!/^\d+$/.test(stateValue)) {
                stateValue = stateValue.replace(/[^\d]/g, '');
            }

            //Добавляем пробелы
            this.stateValue = stateValue.replace(/\s/, '').replace(/\B(?=(\d{3})+(?!\d))/g, ' ');

            //Опредеяем ширину инпута по ширине контента скрытого дива
            this.$nextTick(() => {
                this.inputWidth = `${Math.max(this.$refs.widthInput.offsetWidth + 1, minWidth)}px`;
            });

            this.$emit('input', this.stateValue);
        }
    },

    created() {
        this.stateValue = this.value;
    },

    methods: {
        focus() {
            this.focused = true;
        },
        blur() {
            this.focused = false;
        }
    }
};
</script>

<style lang="scss">
$color-primary: #1a73e8;

.input-group{
    display: flex;
    align-items: center;
    margin-top: 2rem;

    //Также можно было использовать :focus-within, но в IE не поддерживается
    &.-focused{
        .input-group{
            &__picture{
                &::after{
                    border-color: $color-primary;
                }
            }
            &__title{
                color: $color-primary;
            }
            &__input{
                border-color: $color-primary;
            }
        }
    }

    &__picture{
        position: relative;
        width: 60px;
        height: 60px;
        overflow: hidden;
        margin-right: 15px;
        &::after{
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: 2px solid transparent;
            border-radius: 50%;
            transition: border-color .25s ease-in-out;
        }
    }
    &__image{
        max-width: 100%;
        max-height: 100%;
        border-radius: 50%;
    }

    &__content{
        display: flex;
        flex-wrap: wrap;
    }
    &__title{
        font-weight: bold;
        text-transform: uppercase;
        min-width: 100%;
        transition: color .25s ease-in-out;
    }
    &__width{
        position: absolute;
        top: -9999px;
        left: -9999px;
        visibility: hidden;
        font-size: 13px;
        font-weight: bold;
    }
    &__input{
        -webkit-appearance: none;
        -moz-appearance: none;
        height: 30px;
        min-width: 50px;
        width: 50px;
        border: none;
        border-bottom: 2px solid #ddd;
        outline: none !important;
        font-family: inherit;
        font-size: 13px;
        font-weight: bold;
        padding: 0;
        transition: border-color .25s ease-in-out;
        &::-webkit-input-placeholder{
            color: #bbb;
        }
        &:-ms-input-placeholder{
            color: #bbb;
        }
        &::-moz-placeholder{
            color: #bbb;
        }
    }
    &__after-text{
        padding-top: 1px;
        margin-left: 7px;
    }
}
</style>