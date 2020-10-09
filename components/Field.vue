<template>
    <div>
        <b-field grouped multiline>

            <b-field label="Width:" expanded>
                <b-input type="number" :disabled="disabled" v-model="rover.width"></b-input>
            </b-field>

            <b-field label="Height:" expanded>
                <b-input type="number" :disabled="disabled" v-model="rover.height"></b-input>
            </b-field>

        </b-field>

        <b-field grouped multiline>

            <b-field label="Orientation:" expanded>
                <b-input type="text" maxlength="1" :disabled="disabled" v-model="rover.orientation"></b-input>
            </b-field>

            <b-field label="Coordinates:" expanded>
                <b-input type="text" placeholder="X, Y" :disabled="disabled" v-model="rover.coordinates"></b-input>
            </b-field>

        </b-field>

        <b-field label="Movements:" expanded>
            <b-input type="text" :disabled="disabled" v-model="rover.movements"></b-input>
        </b-field>

        <Output :robot="rover"/>
    </div>
</template>

<script>
    import Output from './Output'

    export default {
        name: 'Field',
        components:{
            Output
        },
        data(){
            return {
                disabled: false,
                rover: {
                    width: '',
                    height: '',
                    orientation:'',
                    coordinates: '',
                    movements: ''
                }
            }
        }
    }
</script>