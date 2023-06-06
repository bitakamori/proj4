<script>
export default {
    data() {
        return {
            adv: [],
        };
    },
    methods: {
        getAdvice() {
            fetch("https://api.adviceslip.com/advice")
            .then((res) => res.json())
            .then((data) => {
                this.adv = data;
            });
        },
    },
    mounted(){
        this.getAdvice();
    }
}
</script>

<template>
    <main>
    <table>
    <tr>
    <th>Advice</th>
    </tr>
    <tr v-for="conselho in adv" :key="conselho.advice"> 
    <td>{{ conselho.advice }}</td>
    </tr>
    </table>
    </main>
</template>