<template>
    <div class="view-defi-unlock">
        <h1 class="with-back-btn">
            <f-back-button :route-name="backButtonRoute" />
            Unlock wFTM
        </h1>

        <h2 class="perex">
            Unlock wFTM after you repaid fUSD.
        </h2>

        <defi-deposit
            :token="params.token"
            withdraw
            lock-unlock-mode
            single-token
            token-symbol="WFTM"
            on-submit-route="defi-unlock-confirmation"
        />
    </div>
</template>

<script>
import FBackButton from '@/components/core/FBackButton/FBackButton.vue';
import DefiDeposit from '@/components/DefiDeposit/DefiDeposit.vue';
import { getAppParentNode } from '@/app-structure.js';

export default {
    name: 'DefiUnlock',

    components: { DefiDeposit, FBackButton },

    computed: {
        /**
         * @return {{token: DefiToken}|{}}
         */
        params() {
            const { $route } = this;

            return $route && $route.params ? $route.params : {};
        },

        backButtonRoute() {
            const parentNode = getAppParentNode('defi-unlock');

            return parentNode ? parentNode.route : '';
        },
    },
};
</script>
