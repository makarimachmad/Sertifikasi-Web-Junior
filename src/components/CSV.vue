<template>
    <download-csv
        class   = "btn btn-default"
        :data   = "json_data"
        name    = "filename.csv">
    
        Download CSV (This is a slot)
    
    </download-csv>
</template>
<script>
// import Vue from 'vue'
import JsonCSV from 'vue-json-csv'
 
Vue.component('downloadCsv', JsonCSV)
export default {
    data () {     
        return{
            json_data: [
            {
                'name': 'Tony Peña',
                'city': 'New York',
                'country': 'United States',
                'birthdate': '1978-03-15',
                'phone': {
                    'mobile': '1-541-754-3010',
                    'landline': '(541) 754-3010'
                }
            },
            {
                'name': 'Thessaloniki',
                'city': 'Athens',
                'country': 'Greece',
                'birthdate': '1987-11-23',
                'phone': {
                    'mobile': '+1 855 275 5071',
                    'landline': '(2741) 2621-244'
                }
            }
        ]

        }
    }

}
</script>