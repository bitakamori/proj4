<script>
export default {
    data() {
        return {
            adv: [],
        };
    },
    methods: {
        getAdvice(url) {
            fetch(url)
            .then((res) => res.json())
            .then((data) => {
                this.adv = data;
            });
        },
    },
    mounted(){
        this.getAdvice("https://api.adviceslip.com/advice");
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