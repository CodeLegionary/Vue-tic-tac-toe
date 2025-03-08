<template>
<div class="rules">
    <div class="content">
        <h2>Maybe let's check the rules first?!?</h2>
        <button @click="toggleRules">{{ isRulesVisible ? 'No, thanks' : 'Yes, great idea! &#x1F4A1;' }}</button>
        <div v-if="isRulesVisible">
        <p>
        <strong>Standard Rules:</strong> The game usually sees X as the first player.
        </p>
        <p>
        <strong>Specific Version:</strong> This game follows the standard rules.
        Moreover, this is a classic version and does not foresee any variation of the turns for the whole game.
        So X will be the one to begin the game, as well as each match.
        </p>
        <p>
        <strong>No Time Limit: &#x231B; </strong> ..just have fun
        </p>
        </div>
    </div>
</div>
</template>


<script setup>
import { ref } from 'vue';

const isRulesVisible = ref(false)

function toggleRules() {
    isRulesVisible.value = !isRulesVisible.value
}
</script>


<style scoped>
h2 {
    color: rgb(0, 64, 0);
}

strong {
    color: rgb(40, 30, 51);
}

.rules {
    background-color: #f8f6e0;
    justify-content: center;
    align-items: center;
    display: flex;
}

.content {
    justify-content: center;
}

button {
    padding: 10px 20px;
    margin: 10px 0;
    cursor: pointer;
    font-size: 16px;
    background-color: rgb(147, 255, 219);
    border-radius: 5px;
}

button:hover {
    background-color: rgb(185, 253, 233);
}
</style>