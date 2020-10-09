<template>
    <div>
        <b-field grouped multiline>

            <b-field label="Width:" expanded>
                <b-input type="number" :disabled="disabled" v-model="robot.width"></b-input>
            </b-field>

            <b-field label="Height:" expanded>
                <b-input type="number" :disabled="disabled" v-model="robot.height"></b-input>
            </b-field>

        </b-field>

        <b-field grouped multiline>

            <b-field label="Orientation:" expanded>
                <b-input type="text" maxlength="1" :disabled="disabled" v-model="robot.orientation"></b-input>
            </b-field>

            <b-field label="Coordinates:" expanded>
                <b-input type="text" placeholder="X, Y" :disabled="disabled" v-model="robot.coordinates"></b-input>
            </b-field>

        </b-field>

        <b-field label="Movements:" expanded>
            <b-input type="text" :disabled="disabled" v-model="robot.movements"></b-input>
        </b-field>

        <Output/>
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
                robot:{
                    width: 0,
                    height: 0,
                    orientation:'',
                    coordinates: '',
                    movements: ''
                }
            }
        }
    }
</script>