<template>
    <span class="f-token-value">
        <f-placeholder v-if="usePlaceholder" :content-loaded="!!token.symbol" :replacement-text="replacementText">
            {{ tokenValue }} <span v-if="!noCurrency" class="currency">{{ tokenSymbol }}</span>
        </f-placeholder>
        <template v-else>
            {{ tokenValue }} <span v-if="!noCurrency" class="currency">{{ tokenSymbol }}</span>
        </template>
    </span>
</template>

<script>
import { formatNumberByLocale } from '@/filters.js';
import FPlaceholder from '@/components/core/FPlaceholder/FPlaceholder.vue';

export default {
    name: 'FTokenValue',
    components: { FPlaceholder },
    props: {
        /** @type {DefiToken} */
        token: {
            type: Object,
            default() {
                return {};
            },
            required: true,
        },
        /** Token's value. */
        value: {
            type: [Number, String],
            default: 0,
        },
        /** Hide currency. */
        noCurrency: {
            type: Boolean,
            default: false,
        },
        /** Use FPlaceholder. */
        usePlaceholder: {
            type: Boolean,
            default: true,
        },
        /** Replacement text for FPlaceholder. */
        replacementText: {
            type: String,
            default: '10,000.00 FTM',
        },
    },

    computed: {
        tokenSymbol() {
            return this.$defi.getTokenSymbol(this.token);
        },

        tokenValue() {
            let decimals = this.$defi.tokenDecimals[this.token.symbol];

            return this.value === 0 ? 0 : formatNumberByLocale(parseFloat(this.value).toFixed(decimals), decimals);
        },
    },
};
</script>

<style lang="scss">
@import 'style';
</style>
