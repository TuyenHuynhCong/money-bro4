<template>
    <div class="group1" v-if="!isGame">
        <div class="create">
            <h1> Nhập thông tin</h1>
        </div>
        <div class="child">
            <div class="listPl">
                <div class="pl1">
                    <label for="" class="lb1"> Tên 1</label>
                    <input type="text" v-model="player1" maxlength="10">
                </div>
                <div class="pl2">
                    <label for="" class="lb1"> Tên 2</label>
                    <input type="text" v-model="player2" maxlength="10">
                </div>
                <div class="pl2">
                    <label for="" class="lb1"> Tên 3</label>
                    <input type="text" v-model="player3" maxlength="10">
                </div>
                <div class="pl2">
                    <label for="" class="lb1"> Tên 4</label>
                    <input type="text" v-model="player4" maxlength="10">
                </div>
                <div class="match">
                    <label for="" class="lb1">Số ván</label>
                    <input type="number" v-model="numberMatch">
                </div>
            </div>
            <div class="btn-group">
                <button @click="create" style="height: 25px; margin-right: 10px;">
                    Vào Game
                </button>
                <button @click="reload" style="height: 25px;">
                    Làm mới dữ liệu
                </button>
            </div>
        </div>
    </div>
    <div class="group2" v-if="isGame">
        <!-- <div class="parent"> -->
        <div>
            <table class="table1">
                <tr>
                    <th> #</th>
                    <th>{{ player1 }}</th>
                    <th>{{ player2 }}</th>
                    <th>{{ player3 }}</th>
                    <th>{{ player4 }}</th>
                </tr>
                <tr v-for="index in this.numberMatch" :key="index" class="rowEle">
                    <td>{{ index }}</td>
                    <td><input type="number" style="width: 50px;" class="p1"></td>
                    <td><input type="number" style="width: 50px;" class="p2"></td>
                    <td><input type="number" style="width: 50px;" class="p3"></td>
                    <td><input type="number" style="width: 50px;" class="p4"></td>
                </tr>
                <tr v-if="isShowPoint" class="abc">
                    <th>Tính</th>
                    <th class="pt1">{{ countpl1 }}</th>
                    <th class="pt2">{{ countpl2 }}</th>
                    <th class="pt3">{{ countpl3 }}</th>
                    <th class="pt4">{{ countpl4 }}</th>
                </tr>
                <tr v-if="!isShowPoint">
                    <th>Tính</th>
                    <th></th>
                    <th></th>
                    <th></th>
                    <th></th>
                </tr>
            </table>
        </div>

        <div style="margin-top: 15px;">
            <button @click="count" style="height: 25px; margin-right: 10px;">
                Tính điểm
            </button>
            <button @click="hidden" style="height: 25px; margin-right: 10px;">
                Ẩn điểm
            </button>
            <button @click="back" style="height: 25px; margin-right: 10px;">
                Thoát
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
            numberMatch: Number,
            isGame: false,
            countpl1: 0,
            countpl2: 0,
            countpl3: 0,
            countpl4: 0,
            isShowPoint: false,
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
        create() {
            if (!this.player1 || !this.player2 || !this.player3 || !this.player4 || !this.numberMatch || this.numberMatch <= 0  ) {
                alert('Vui lòng nhập đủ thông tin hoặc số ván phải là số nguyên > 0 ')
                return;
            }

            const array = [this.player1, this.player2, this.player3, this.player4];

            let check = array.filter((e, i, a) => a.indexOf(e) === i)
            if (check.length != 4) {
                alert('Vui lòng nhập tên người chơi không trùng lặp')
                return;
            }

            this.isGame = true;
        },
        count() {
            this.countpl1 = 0;
            this.countpl2 = 0;
            this.countpl3 = 0;
            this.countpl4 = 0;
            // this.isShowPoint = false
            var rowEle = document.querySelectorAll('.rowEle');
            // Set their ids
            for (var i = 0; i <= rowEle.length; i++) {
                if (rowEle[i]) {
                    let pl1 = rowEle[i].getElementsByClassName('p1')[0].value;
                    this.countpl1 += Number(pl1);
                    let pl2 = rowEle[i].getElementsByClassName('p2')[0].value;
                    this.countpl2 += Number(pl2);
                    let pl3 = rowEle[i].getElementsByClassName('p3')[0].value;
                    this.countpl3 += Number(pl3);
                    let pl4 = rowEle[i].getElementsByClassName('p4')[0].value;
                    this.countpl4 += Number(pl4);
                }
            }
            // highlight 
            //pl1
            if (this.orderNumber(this.countpl1, this.countpl2, this.countpl3, this.countpl4) == 1 || this.orderNumber(this.countpl1, this.countpl2, this.countpl3, this.countpl4) == 2) {
                this.setColor('.pt1');
            } else {
                this.replaceColor('.pt1');
            }
            // pl2
            if (this.orderNumber(this.countpl2, this.countpl1, this.countpl3, this.countpl4) == 1 || this.orderNumber(this.countpl2, this.countpl1, this.countpl3, this.countpl4) == 2) {
                this.setColor('.pt2');
            } else {
                this.replaceColor('.pt2');
            }
            //pl3
            if (this.orderNumber(this.countpl3, this.countpl1, this.countpl2, this.countpl4) == 1 || this.orderNumber(this.countpl3, this.countpl1, this.countpl2, this.countpl4) == 2) {
                this.setColor('.pt3');
            } else {
                this.replaceColor('.pt3');
            }
            //pl4
            this.orderNumber(this.countpl4, this.countpl1, this.countpl2, this.countpl3);
            if (this.orderNumber(this.countpl4, this.countpl1, this.countpl2, this.countpl3) == 1 || this.orderNumber(this.countpl4, this.countpl1, this.countpl2, this.countpl3) == 2) {
                this.setColor('.pt4');
            } else {
                this.replaceColor('.pt4');
            }
            this.isShowPoint = true;
        },
        setColor(className) {
            setTimeout(() => {
                var element = document.querySelector(className);
                element.className = element.className.replaceAll("br-red", "");
                element.className += ' br-red';
            }, "10");
        },
        replaceColor(className) {
            setTimeout(() => {
                var element = document.querySelector(className);
                element.className = element.className.replaceAll("br-red", "")
            }, "100");
        },
        // 2,4,1,3
        orderNumber(plcurrent, pl1, pl2, pl3) {
            let value = plcurrent;
            let index = 1;
            if (value > pl1) {
                index = index + 1;
            }
            if (value > pl2) {
                index = index + 1;
            }
            if (value > pl3) {
                index = index + 1;
            }
            return index;
        },
        hidden() {
            if (this.isShowPoint) {
                this.isShowPoint = !this.isShowPoint;
            }
        },
        back() {
            if (confirm('Bạn chắc chắn muốn thoát ?')) {
                this.isGame = false;
                this.player1 = '';
                this.player2 = '';
                this.player3 = '';
                this.player4 = '';
                this.numberMatch = '';
                this.countpl1 = 0;
                this.countpl2 = 0;
                this.countpl3 = 0;
                this.countpl4 = 0;
                this.isShowPoint = false;
            }

        }
    }
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.br-red {
    background-color: red;
}

.table1 {
    display: inline-table;
}

table,
th,
td {
    border: 1px solid black;
    border-collapse: collapse;
}

table,
th {
    width: 10px;
}

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
}
</style>
  