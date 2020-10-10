<template>
    <div>
        <b-field class="has-text-centered">

            <b-button type="is-info" :disabled="disabled" 
                :loading="loading" @click="validateCommands">
                Init Test
            </b-button>

        </b-field>
    </div>
</template>

<script>
    export default {
        name: 'Output',
        props: {
            robot: Object
        },
        data(){
            return {
                results: [],
                loading: false,
            }
        },
        computed:{
            disabled(){
                if (!this.robot.width || !this.robot.height || !this.robot.orientation || !this.robot.coordinates || !this.robot.movements) {
                    return true
                }
                return false
            }
        },
        methods: {
            removeWhiteSpace(s) {
                return s.replace(/\s+/g, '').trim()
            },

            stringOrientation(orientation){
                switch(orientation){
                    case 'N':
                        return 'North'
                    case 'S':
                        return 'South'
                    case 'E':
                        return 'East'
                    case 'W':
                        return 'West'
                    default:
                        break
                }
            },

            validateCommands() {

                this.loading = true
                
                let rover = {
                    orientation: this.removeWhiteSpace(this.robot.orientation).toUpperCase(),
                    x: Number(this.removeWhiteSpace(this.robot.coordinates.x)),
                    y: Number(this.removeWhiteSpace(this.robot.coordinates.y))
                }

                const array = this.removeWhiteSpace(this.robot.movements.toUpperCase()).split('')
                
                let valid = true
                
                for (let i = 0; i < array.length; i++) {
                    const movement = array[i]
                    switch (rover.orientation) {
                        case 'N':
                            if (movement === 'A') {
                                valid = rover.y + 1 <= this.robot.height
                                valid && rover.y++
                            } else if (['L','R'].indexOf(movement) !== -1){
                                rover.orientation = movement === 'L' ? 'W' : 'E'
                            } else {
                                valid = false
                            }
                            break
                        case 'S':
                            if (movement === 'A') {
                                valid = rover.y - 1 >= 0
                                valid && rover.y--
                            } else if (['L','R'].indexOf(movement) !== -1){
                                rover.orientation = movement === 'L' ? 'E' : 'W'
                            } else {
                                valid = false
                            }
                            break
                        case 'E':
                            if (movement === 'A') {
                                valid = rover.x + 1 <= this.robot.width
                                valid && rover.x++
                            } else if (['L','R'].indexOf(movement) !== -1){
                                rover.orientation = movement === 'L' ? 'N' : 'S'
                            } else {
                                valid = false
                            }
                            break
                        case 'W':
                            if (movement === 'A') {
                                valid = rover.x - 1 >= 0
                                valid && rover.x--
                            } else if (['L','R'].indexOf(movement) !== -1){
                                rover.orientation = movement === 'L' ? 'S' : 'N'
                            } else {
                                valid = false
                            }
                            break
                        default:
                            valid = false
                            break
                    }
                    if (!valid) {
                        this.$buefy.toast.open({
                            message: 'Data Error!',
                            type: 'is-danger'
                        })
                        break
                    }

                    if(i===0)
                        this.results.push('Valid: ' + `${valid}, `.toUpperCase() + 'Orientation: ' + this.stringOrientation(`${rover.orientation}`) + `, Coordenates: (${rover.x},${rover.y}).`)
                    else
                        this.results.push('\nValid: ' + `${valid}, `.toUpperCase() + 'Orientation: ' + this.stringOrientation(`${rover.orientation}`) + `, Coordenates: (${rover.x},${rover.y}).`)
                }

                this.$emit('response', this.results)
                this.loading = false
            }
        }
    }
</script>
