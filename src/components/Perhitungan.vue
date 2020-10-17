<template>
  <v-container
    class="px-0"
    fluid
  > 
    <bar-chart></bar-chart>
    <br>
    <div>
        <ul>
            <li v-text="'persegi = '+ this.banyak.persegi + ' | ' + this.prosentase.persegi+' %'"></li>
            <li v-text="'segitiga = '+ this.banyak.segitiga + ' | ' + this.prosentase.segitiga+' %'"></li>
            <li v-text="'lingkaran = '+ this.banyak.lingkaran + ' | ' + this.prosentase.lingkaran+' %'"></li>
        </ul>
    </div>
    <br><br>
    <vue-json-to-csv
        :json-data="[ this.jenis]">
    </vue-json-to-csv>
    <v-radio-group >
      <v-radio
        v-for="n in jenis"
        :key="n"
        :label="`${n}`"
        :value="n"
        @click="pilihBidang(n)"
      ></v-radio>
    </v-radio-group>
    <v-form  v-if="persegi===true" @submit.prevent="hitungPersegi">
        <v-container>
        <v-row>
            <v-col
            cols="12"
            md="4"
            >
            <v-text-field
                v-model="bpersegi.p"
                label="Panjang"
            ></v-text-field>
            </v-col>

            <v-col
            cols="12"
            md="4"
            >
            <v-text-field
                v-model="bpersegi.l"
                label="Lebar"
                required
            ></v-text-field>
            </v-col>
            <v-col>
                <v-btn
                    color="primary"
                    type="submit"
                >Hitung</v-btn>
            </v-col>
        </v-row>
        </v-container>
    </v-form>
    <v-form  v-if="segitiga===true" @submit.prevent="hitungSegitiga">
        <v-container>
        <v-row>
            <v-col
            cols="12"
            md="4"
            >
            <v-text-field
                v-model="bsegitiga.a"
                label="alas"
            ></v-text-field>
            </v-col>

            <v-col
            cols="12"
            md="4"
            >
            <v-text-field
                v-model="bsegitiga.t"
                label="tinggi"
                required
            ></v-text-field>
            </v-col>
            <v-col>
                <v-btn
                    color="primary"
                    type="submit"
                >Hitung</v-btn>
            </v-col>
        </v-row>
        </v-container>
    </v-form>
    <v-form  v-if="lingkaran===true" @submit.prevent="hitungLingkaran">
        <v-container>
        <v-row>
            <v-col
            cols="12"
            md="4"
            >
            <v-text-field
                v-model="blingkaran.r"
                label="Jari-Jari"
            ></v-text-field>
            </v-col>

            <v-col>
                <v-btn
                    color="primary"
                    type="submit"
                >Hitung</v-btn>
            </v-col>
            
        </v-row>
        </v-container>
    </v-form>
    <v-card v-if="bantu===true">
        <div v-text="'Hasil = '+nilai"></div>
        
    </v-card>
    
  </v-container>
  
  
</template>
<script>
import BarChart from '@/components/BarChart'
import VueJsonToCsv from 'vue-json-to-csv'
  export default {
    components: {
        BarChart,
        VueJsonToCsv
    },
    data () {
      return {
        
        bantu:false,
        nilai:'',
        gabung:[
            {
                jenis:["","",""],
                nilai:[]
            }
        ],
        bpersegi:{
            p:'',
            l:'',
            nilaipersegi:0
        },
        blingkaran:{
            r:'',
            nilailingkaran:0
        },
        bsegitiga:{
            a:'',
            t:'',
            nilaisegitiga:0
        },
        banyak:{
            persegi:0,
            segitiga:0,
            lingkaran:0
        },
        jenis:["segitiga","lingkaran","persegi"],
        segitiga:false,
        persegi:false,
        lingkaran:false,
        prosentase:{
            persegi:0.0,
            segitiga:0.0,
            lingkaran:0.0
        }
      }
    },
    methods: {
        pilihBidang(n){
            console.log(n)
            if (n=="segitiga"){
                this.segitiga=true
                this.persegi=false
                this.lingkaran=false
                this.bantu=false
            }else if(n=="persegi"){
                this.segitiga=false
                this.persegi=true
                this.lingkaran=false
                this.bantu=false
            }else{
                 this.segitiga=false
                this.persegi=false
                this.lingkaran=true
                this.bantu=false
            }
        },
        hitungPersegi(){
            //console.log("berhasil")
            this.bantu=true
            this.nilai=this.bpersegi.p*this.bpersegi.l
            this.bpersegi.nilaipersegi=this.bpersegi.p*this.bpersegi.l
            this.banyak.persegi = this.banyak.persegi+1
            this.prosentase.persegi = this.banyak.persegi /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            this.prosentase.lingkaran = this.banyak.lingkaran /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            this.prosentase.segitiga = this.banyak.segitiga /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            console.log(this.bpersegi)
            console.log(this.banyak)
        },
        hitungSegitiga(){
            //console.log("berhasil")
            this.bantu=true
            this.nilai=0.5*this.bsegitiga.a*this.bsegitiga.t
            this.bsegitiga.nilaisegitiga=0.5*this.bsegitiga.a*this.bsegitiga.t
            this.banyak.segitiga=this.banyak.segitiga+1
            this.prosentase.segitiga = this.banyak.segitiga /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            this.prosentase.lingkaran = this.banyak.lingkaran /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            this.prosentase.persegi = this.banyak.persegi /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            console.log(this.bsegitiga)
            console.log(this.banyak)
        },
        hitungLingkaran(){
            //console.log("berhasil")
            this.bantu=true
            this.nilai=3.14*this.blingkaran.r*this.blingkaran.r
            this.blingkaran.nilailingkaran=3.14*this.blingkaran.r*this.blingkaran.r
            this.banyak.lingkaran=this.banyak.lingkaran+1
            this.prosentase.lingkaran = this.banyak.lingkaran /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            this.prosentase.persegi = this.banyak.persegi /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            this.prosentase.segitiga = this.banyak.segitiga /(this.banyak.persegi+this.banyak.segitiga+this.banyak.lingkaran)*100
            console.log(this.blingkaran)
            console.log(this.banyak)
        }
    }
  }
</script>
