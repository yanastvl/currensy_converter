<template>
    <div class="wrapper__column">
        <p class="wrapper__text">{{ caption }}</p>
        <div class="wrapper__input">
            <img class="wrapper__img" :src="`https://ipdata.co/flags/${locale}.png`" alt="">
            <select class="wrapper__select" v-model="selected" @change="updateCountry">
                <option v-for="country in countryList" :key="country">
                    {{ country }}
                </option>
            </select>
        </div>
    </div>
</template>


<style lang="scss" scoped>
    .wrapper{
    &__column{
        width: 40%;
        padding-bottom: 20px;
    }

    &__input{
        display: flex;
        align-items: center;
        justify-content: space-between;
    
        border: 2px solid #dbe1e6;
        border-radius: 5px;
        outline: none;
        padding: 5px 10px;
    
        height: 50px;
        width: 100%;
    }

    &__text{
        font-size: 20px;
        line-height: 19px;
        padding-bottom: 10px;
    }
    
    &__select{
        appearance: auto;
        outline: none;
    }

    &__img{
        padding-right: 5px;
    }
    
    }
</style>

<script>
import FlagsMap from '../flags.js';

    export default {
        data() {
            return {
                locale: "ru"
            };
        },
        methods: {
            updateCountry(e) {
                this.$emit('setCountry', e.target.value, this.caption);
            }
        },
        computed: {
            selected() {
                this.locale = FlagsMap[this.selectedCountry];
                return this.selectedCountry
            }
        },
        props: ["caption", "countryList", "selectedCountry"],
    }
</script>
