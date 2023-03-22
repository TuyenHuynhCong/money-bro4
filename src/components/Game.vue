<template>
    <div class="create">
        <h1> Nhập thông tin</h1>
    </div>
    <div class="child">
        <div class="listPl">
            <div class="pl1">
                <label for="" class="lb1"> Tên 1</label>
                <input type="text" v-model="player1">
            </div>
            <div class="pl2">
                <label for="" class="lb1"> Tên 2</label>
                <input type="text" v-model="player2">
            </div>
            <div class="pl2">
                <label for="" class="lb1"> Tên 3</label>
                <input type="text" v-model="player3">
            </div>
            <div class="pl2">
                <label for="" class="lb1"> Tên 4</label>
                <input type="text" v-model="player4">
            </div>
            <div class="match">
                <label for="" class="lb1">Số ván</label>
                <input type="number" v-model="numberMatch">
            </div>
        </div>
        <div class="btn-group">
            <button @click="create1" style="height: 25px; margin-right: 10px;">
                Create
            </button>
            <button @click="reload" style="height: 25px;">
                Reload
            </button>
        </div>
    </div>
</template>
  
<script>
export default {
    name: 'CreatePlayer',
    data() {
        return {
            player1: '',
            player2: '',
            player3: '',
            player4: '',
            numberMatch: Number
        }
    },
    props: {
        //   msg: String
    },
    methods: {
        reload() {
            this.player1 = '';
            this.player2 = '';
            this.player3 = '';
            this.player4 = '';
            this.numberMatch = '';
        },
        create1(){

        }
    }
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.lb1 {
    margin-right: 2rem;
}

.btn-group {
    margin-top: 3rem;
}

.pl1 {
    padding: 20px;

}

.match {
    margin-left: -10px;
}

.pl2 {
    padding: 10px 10px 10px 40px;
    margin-right: 2rem;

}

.create {
    margin-top: 150px;
}

.child {
    border-style: solid;
    height: 300px;
}

h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}</style>
  