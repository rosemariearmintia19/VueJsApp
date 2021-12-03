<template>
<div class="hello">
    <span>Transactions</span><br>
    <input v-model="value" type="number">
    <button @click="GetAverage()">Submit</button>
    <p>
        Average : {{average}}
    </p>
    <br>
    <br>
    <center>
        <table border="1px solid">
            <thead>
                <tr>
                    <th>Transaction</th>
                    <th>Average</th>
                </tr>

            </thead>
            <tbody>
                <tr v-for="(list, n) in outputs" :key="n">
                    <td>{{list.new}}</td>
                    <td>{{list.average}}</td>
                </tr>
            </tbody>
        </table>
    </center>

</div>
</template>

<script>
export default {
    name: 'HelloWorld',
    data() {
        return {
            value: "",
            oldValue: 0,
            newValue: 0,
            average: 0,
            outputs: [],
            new_ave : 0,
        }
    },
    mounted() {
        this.outputs = JSON.parse(localStorage.getItem('lists'));

    },
    watch: {
        value(newValue, oldValue) {
            this.oldValue = oldValue,
            this.newValue = newValue
        }

    },
    methods: {
        GetAverage() {

            var Transactions = {
                "old": this.oldValue,
                "new": this.newValue,
                "average": (parseInt(this.newValue) + parseInt(this.oldValue)) / 2

            };

            var lists = [];
            lists.push(Transactions);
            this.outputs = lists;

            if (this.oldValue) {
                this.average = (parseInt(this.newValue) + parseInt(this.oldValue)) / 2
                this.value = ''
                this.saveNums()
            } else {
                this.average = this.newValue
                this.value = ''
                this.saveNums()
            }

            // this.new_ave = (parseInt( this.average) + parseInt(this.newValue)) / 2
            // console.log()
        },
        saveNums() {
            const parsed = JSON.stringify(this.outputs);
            localStorage.setItem('outputs', parsed);
        }
    }
}
</script>


<style scoped>

</style>
