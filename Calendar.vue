<template>
    <div class="home">
        <h1>Takvim</h1>
        <div>
        <span>{{ guncelAy }} - </span><span>{{ guncelYil }}</span>
        </div>
        <div class="calendar">
            <div class="tarihler">
                <div class="gunler">
                    <span>Pt</span>
                    <span>Sa</span>
                    <span>Ça</span>
                    <span>Pe</span>
                    <span>Cu</span>
                    <span>Ct</span>
                    <span>Pa</span>
                </div>
                <div class="sayilar">
                    <span 
                    :id="[ i == 1 ? 'basis' : '']"
                    :style="[i == new Date().getDate() && guncelAy == aylar[new Date().getMonth()] ? guncelCss : {'color': 'black'}]"
                    :key="i" v-for="i in guncelGunSayisi"> {{ i }} </span>
                </div>
                <div class="guncelle">
                    <span @click="geriGit">Geri</span> 
                    <span @click="ileriGit">İleri</span>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
    var d = new Date();
    var gun = d.getDay()
    var ay = d.getMonth();
    var yil = d.getFullYear();
    var aylikSayilar = new Date(yil, ay+1, 0).getDate();
    export default {
        data() {
            return {
                aylar: ["Ocak", "Şubat", "Mart", "Nisan", "Mayıs", "Haziran", "Temmuz", "Ağustos", "Eylül", "Ekim", "Kasım", "Aralık"],
                gunler: ["Pazar", "Pazartesi", "Salı", "Çarşamba", "Perşembe", "Cuma", "Cumartesi"],
                guncelGun: "",
                guncelAy: "",
                guncelYil: "",
                guncelGunSayisi: "",
                simdikiAy: "",
                guncelCss: {
                    'border': '1px solid orangered',
                    'box-shadow': '1px 1px 9px 1px orangered'
                }
            }
        },
        mounted() {
            this.simdikiAy = ay;
            this.guncelAy = this.aylar[ay];
            this.guncelYil = yil;
            this.guncelGunSayisi = aylikSayilar;
            this.guncelGun = this.gunler[gun];

            var date = new Date(yil, ay, 1); 
            var baslangicGun = date.getDay() - 1;
            if(baslangicGun == -1 ){
                baslangicGun = 6;
            }
            document.documentElement.style.setProperty("--margin", baslangicGun);
        },
        methods: {
            geriGit() {
                ay--;
                aylikSayilar--;
                if(ay < 0){
                    yil--;
                    ay= 11;
                }
                this.guncelAy = this.aylar[ay];
                this.guncelGunSayisi = new Date(yil, ay+1, 0).getDate();
                this.guncelYil = yil;
                var date = new Date(yil, ay, 1); 
            var baslangicGun = date.getDay() - 1;
            if(baslangicGun == -1 ){
                baslangicGun = 6;
            }
            document.documentElement.style.setProperty("--margin", baslangicGun);

            },
            ileriGit() {
                ay++;
                aylikSayilar++;
                if(ay > 11){
                    yil++;
                    ay= 0;
                }
                this.guncelAy = this.aylar[ay];
                this.guncelGunSayisi = new Date(yil, ay+1, 0).getDate();
                this.guncelYil = yil;
                var date = new Date(yil, ay, 1); 
            var baslangicGun = date.getDay() - 1;
            if(baslangicGun == -1 ){
                baslangicGun = 6;
            }
            document.documentElement.style.setProperty("--margin", baslangicGun);
            }
        },
    }

</script>

<style scoped>
    .home {
        width: 100%;
        min-height: 80vh;
        height: auto;
        background-color: teal;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }


    .calendar {
        width: 400px;
        height: 400px;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .calendar .tarihler {
        width: 350px;
        height: 350px;
    }

    .calendar .tarihler .gunler {
        display: flex;
        justify-content: space-between;
    }

    .calendar .tarihler .gunler span {
        width: 45px;
        text-align: center;
    }

    .calendar .tarihler .sayilar {
        display: flex;
        justify-content: flex-start;
        flex-wrap: wrap;
        cursor: pointer;
    }

    .calendar .tarihler .sayilar span {
        width: 45px;
        text-align: center;
        margin-top: 10px;
        margin-right: 3px;
        line-height: 40px;
        border: 1px solid black;
    }

    .calendar .tarihler .sayilar span:hover {
        border: 1px solid orangered;
        box-shadow: 1px 1px 9px 1px orangered;
    }

    .active {
        color: red;
        background-color: red;
    }

    .guncelle {
        margin-top: 20px;
        display: flex;
        justify-content: space-between;
    }

    .guncelle span {
        cursor: pointer;
    }

    .guncelle span:hover {
        color: white;
    }

    #basis {
        margin-left: calc(var(--margin) * 50px);
    }

   
</style>