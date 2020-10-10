<template>
    <div>

        <div class="columns is-centered">

            <div class="column is-4 is-narrow">

                <h3 class="subtitle is-3 has-text-centered is-italic">Field</h3>

                <b-field horizontal expanded>

                    <template slot="label">
                        Width:
                    </template>

                    <b-input type="number" :disabled="disabled" v-model="rover.width"></b-input>
                
                </b-field>

                <b-field horizontal expanded>

                    <template slot="label">
                        Height:
                    </template>

                    <b-input type="number" :disabled="disabled" v-model="rover.height"></b-input>
                
                </b-field>
            
            </div>

            <div class="column is-4">
                
                <h3 class="subtitle is-3 has-text-centered is-italic">Initial Position</h3>

                <b-field horizontal expanded>
                    
                    <template slot="label">
                        Orientation:
                    </template>
                    
                    <b-select v-model="rover.orientation" expanded>
                        <option value="N">North</option>
                        <option value="S">South</option>
                        <option value="E">East</option>
                        <option value="N">West</option>
                    </b-select>
                
                </b-field>


                <b-field label="Coordenates:" position="is-centered" expanded>

                    <b-field horizontal expanded>
                        <template slot="label">
                            X:
                        </template>
                        
                        <b-input type="number" placeholder="X" :disabled="disabled" 
                            v-model="rover.coordinates.x">
                        </b-input>
                    
                    </b-field>

                    <b-field horizontal expanded>
                        <template slot="label">
                            Y:
                        </template>
                        
                        <b-input type="number" placeholder="Y" :disabled="disabled" 
                            v-model="rover.coordinates.y">
                        </b-input>

                    </b-field>

                </b-field>
            </div>

        </div>


        <div class="columns is-centered">

            <div class="column is-5">

                <b-field horizontal position="is-centered">
                    <template slot="label" class="has-text-left">
                        Movements:
                    </template>
                    
                    <b-input type="text" :disabled="disabled" 
                        v-model="rover.movements"></b-input>
                
                </b-field>
            
            </div>

            <div class="column is-3">
                <Output :robot="rover" v-on:response="response" />
            </div>

        </div>

        <div class="columns">
            <div class="column is-2">
            </div>

            <div class="column is-7">
                <b-field horizontal position="is-centered" type="is-info">
                    <template slot="label" class="has-text-left">
                        Result:
                    </template>
                    
                    <b-input type="textarea" disabled="true" v-model="result"></b-input>
                
                </b-field>
            
            </div>
        
        </div>
        
    </div>
</template>

<script>
    import Output from './Output'

    export default {
        name: 'Field',
        components: {
            Output
        },
        data() {
            return {
                disabled: false,
                result: '',
                rover: {
                    width: '',
                    height: '',
                    orientation: 'N',
                    coordinates: {
                        x: '',
                        y: ''
                    },
                    movements: ''
                }
            }
        },
        methods: {
            response(r) {
                this.result = ''
                this.result = r;
            }
        }
    }
</script>