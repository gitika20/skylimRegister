<template>
    <div id="app" >
        <v-app id="inspire" style="background-color:white">
            <navbar class="mb-2"></navbar>

               <v-layout row wrap >
                   <v-flex lg8 offset-lg2>

                       

                    <v-stepper v-model="e1"  style="box-shadow:0 0 0 0;background-color:#E9EBEE;">
                        <v-stepper-header style="box-shadow:1px 0 0.5px 0">
                             <v-stepper-step step="1" :complete="e1 > 1" editable></v-stepper-step>
                            <v-divider></v-divider>
                            <v-stepper-step step="2" :complete="e1 > 2" editable></v-stepper-step>
                            <v-divider></v-divider>
                            <v-stepper-step step="3" :complete="e1 > 3" editable></v-stepper-step>
                            <v-divider></v-divider>
                            <v-stepper-step step="4" editable></v-stepper-step>
                            <v-divider></v-divider>
                            <v-stepper-step step="5" editable></v-stepper-step>
                        </v-stepper-header>
                        
                        <v-stepper-items style="padding:0px" >
                            <v-stepper-content step="1" style="width:100%;padding:0px;margin:0px" >
                                <intro></intro>
                                <v-btn color="primary" @click.native="e1 = 2">go to registration</v-btn>                        
                            </v-stepper-content>
                            <v-stepper-content step="2" style="width:100%;padding:0px;margin:0px" >
                                <one :complete="e1" @form1validity="setE" ></one>
                            </v-stepper-content>
                            <v-stepper-content step="3">
                                <two :complete="e1" @form1validity="setE"></two>
                                <v-btn color="primary" @click.native="e1 = 2">Go Back</v-btn>                        
                            </v-stepper-content>
                            <v-stepper-content step="4">
                                <three :complete="e1" @to1push="pushing" @form1validity="setE"></three>
                                <v-btn color="primary"  @click.native="e1 = 3">Go back</v-btn>
                            </v-stepper-content>
                              <v-stepper-content step="5">
                                <four></four>
                                <v-btn color="primary" @click.native="e1 = 1">Continue</v-btn>
                                <v-btn flat>Cancel</v-btn>
                            </v-stepper-content>
                        </v-stepper-items>
                
                    
                    </v-stepper>
            </v-flex>
            </v-layout>
        </v-app>
    </div>
</template>
  
<script>

import navbar from './../navbar.vue'

import one from './steps/one.vue'
import two from './steps/two.vue'
import three from './steps/three.vue'
import four from './steps/four.vue'
import intro from './steps/intro.vue'
import {mapActions} from 'vuex';

export default {
  data () {
    return {
      e1: 0,
        combine:[]
    }
  },
    computed: {
        form(){
            return this.$store.state.form;
        },
        allstudents(){
            return this.$store.state.allstudents;
        }
    },
    methods:{
        setE(val){
            this.e1=parseInt(val);
        },
        pushing:function(arg){
            this.$store.commit('pushing',arg)
        },
  },
  components:{navbar,one,two,three,four,intro}
}
</script>