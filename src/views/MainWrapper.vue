<template>
    <section class="wrapper">
        <h1 class="wrapper__title">Currency Converter</h1>
        <h2 class="wrapper__subtitle">Source: CBR</h2>
        <div class="wrapper__inner">
            <div class="wrapper__column--first">
                <p class="wrapper__text">Enter the Amount</p>
                <input class="wrapper__input" type="number" autocomplete="off" v-model="amount" @input="setAmount">
            </div>
            <div class="wrapper__column--second">

                <Selection caption="From:" :countryList="countryList" @setCountry="setCountry" :selectedCountry="FromCountry"></Selection>

                <button class="wrapper__button" @click="swapCurrency">

                <svg class="wrapper__icon" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 1000 1000" enable-background="new 0 0 1000 1000" xml:space="preserve">
                <metadata> Svg Vector Icons : http://www.onlinewebfonts.com/icon </metadata>
                <g><path d="M955.1,481.5c4.3,46.6,4.1,90.1-4.4,133.4c-14.3,72.4-47.2,134.1-107.7,179.5c-44.9,33.7-96.3,52.9-151.9,57.8c-48,4.2-96.4,4-144.6,4.4c-79.3,0.6-158.6,0.3-237.9-0.2c-10.4-0.1-14,2.4-13.8,13.3c0.7,35.4,0.3,70.8,0.3,106.2v14.2C198.9,910.4,105.3,832.8,10,753.7c94.8-78.6,188.4-156.3,284.2-235.7c0.3,5.8,0.7,9.4,0.7,12.9c0,36.1,0.3,72.2-0.2,108.3c-0.1,9.1,2.6,12.1,11.9,12.1c105.4-0.5,210.8,0.7,316.1-1.5c77.3-1.6,152.9-15,222.4-51.2c38.3-20,71.1-46.4,93.3-83.8C944.3,505.1,948.7,494.5,955.1,481.5z M703.8,479.7c0-22.5,0-45,0-67.5c0-17.7-0.2-35.4,0.2-53.1c0.2-7.8-2.8-10.1-10.5-10.1c-108.2,0.6-216.4-0.5-324.5,2c-74.5,1.7-147.1,15.5-214.2,49.9c-36.8,18.8-68.7,43.7-91.2,78.7c-6.9,10.8-12.2,22.5-19.2,35.6c-0.8-9.2-1.7-17.1-2.1-25c-3.4-66.9,5.2-131.7,36.6-192.1c42.4-81.6,112.3-126.7,201.5-145.6c36.1-7.6,72.6-8.6,109.3-8.6c100.8,0.1,201.6-0.1,302.4,0.3c9.9,0,11.5-3.5,11.4-12.1c-0.4-36.1-0.1-72.2-0.1-108.3v-14c96.7,80,191.1,158,286.6,237c-95.2,78.8-189.3,156.6-283.3,234.4C705.7,480.7,704.8,480.2,703.8,479.7z"/></g>
                </svg>
                </button>
            
                <Selection caption="To:" :countryList="countryList" @setCountry="setCountry" :selectedCountry="ToCountry"></Selection>

            </div>
        </div>
        <div class="wrapper__total">
            <p class="wrapper__total--text"> {{ resultText }}
            </p>
        </div>
    </section>    
</template>


<style lang="scss" scoped>
    .wrapper{
    padding: 40px;
    width: 370px;
    height: auto;
    background-color: #f2f3f4;
    border: 1px solid #ccc;
    border-radius: 10px;
    box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;

    &__inner{
        display:flex;
        flex-direction: column;
        justify-content:space-between;
        align-items:center;
    }

    &__title{
        padding-bottom: 10px;
        font-size: 28px;
        line-height: 25px;
        text-align: center;
    }

    &__subtitle{
        padding-bottom: 20px;
        text-align: center;
        font-size: 16px;
        line-height: 18px;
        color:grey;

    }

    &__text{
        font-size: 20px;
        line-height: 19px;
        padding-bottom: 10px;

    }

    &__column{
        width: 40%;
        padding-bottom: 20px;

        &--first{
        width: 100%;
        padding-bottom: 20px;
        }

        &--second{
            width: 100%; 
            display: flex;
            flex-direction: row;
            justify-content:space-between;
        }
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

    &__select{
        appearance: auto;
        outline: none;
    }

    &__total{
        min-height: 110px;
        border: 1px solid #dbe1e6;
        border-radius: 0.5rem;
        padding: 2.5rem;
        text-align: center;

        &--text{
            font-size:18px;
            font-weight: 500;
        }
    }

    &__icon{
        width: 30px;
        display: flex;
        align-self: center;
        cursor:pointer;
    }
    }


</style>

<script>
import Selection from '../components/Selection.vue'

export default {
    data() {
            return {
                countryCurrencyMap: {},
                countryList: [],
                amount: 1,
                resultText: "",
                FromCountry: localStorage.getItem("From:"),
                ToCountry: localStorage.getItem("To:")
            };
        },
    mounted() {
            const axios = require('axios').default;
            axios
            .get('https://cdn.cur.su/api/cbr.json')
            .then(response => (
                    this.countryCurrencyMap = response["data"]["rates"],
                    this.countryList = Object.keys(this.countryCurrencyMap),
                    this.countryList.sort(),
                    delete this.countryList[33],
                    this.countryList = this.countryList.filter(entry => entry.trim() != ''),
                    this.calcCurrency()
                )
            );
        },
    methods: {
        getCurrencyFromBrowserLocale() {
            const localeCurrency = require('locale-currency');
            let locale = window.navigator.language || window.navigator.userLanguage;
            return localeCurrency.getCurrency(locale);
        },
        setCountry(country, caption) {
            localStorage.setItem(caption, country);
            this.calcCurrency();
		},
        setAmount() {
            localStorage.setItem("amount", this.amount);
            this.calcCurrency();
        },
        calcCurrency() {
            let currencyFromBrowserLocale = this.getCurrencyFromBrowserLocale();
            this.amount = localStorage.getItem("amount") ? localStorage.getItem("amount") : this.amount;
            this.FromCountry = localStorage.getItem("From:") ? localStorage.getItem("From:") : currencyFromBrowserLocale;
            let FromValue = this.countryCurrencyMap[this.FromCountry];
            this.ToCountry = localStorage.getItem("To:") ? localStorage.getItem("To:") : "USD";
            let ToValue = this.countryCurrencyMap[this.ToCountry];
            let result = this.amount*ToValue/FromValue;
            result = result.toFixed(4);
            this.resultText = `${this.amount} ${this.FromCountry} = ${result} ${this.ToCountry}`
        },
        swapCurrency() {
            const temp = this.ToCountry;
            this.setCountry(this.FromCountry, "To:");
            this.setCountry(temp, "From:");
        },
    },
    components: { Selection }
}
</script>
