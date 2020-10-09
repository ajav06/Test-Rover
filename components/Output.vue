<template>
    <div>
        <b-field class="has-text-centered">
            <b-button type="is-info" :disabled="disabled" @click="validateCommands">Init Test</b-button>
        </b-field>

        {{ robot.width }}
    </div>
</template>

<script>
    export default {
        name: 'Output',
        props: {
            robot: Object
        },
        computed:{
            disabled(){
                if (!this.robot.width || !this.robot.height || !this.robot.orientation || !this.robot.coordinates || !this.robot.movements) {
                    return true
                }
                return false;
            }
        },
        methods: {
            removeWhiteSpace(s) {
                return s.replace(/\s+/g, '').trim();
            },

            validateCommands() {
                if (this.disabled) {
                    return 'Error -> Please enter all data'
                }

                let rover = {
                    orientation: this.removeWhiteSpace(this.robot.orientation).toUpperCase(),
                    x: Number(this.removeWhiteSpace(this.robot.coordinates).split(',')[0]),
                    y: Number(this.removeWhiteSpace(this.robot.coordinates).split(',')[1])
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
                            } else {
                                rover.orientation = movement === 'L' ? 'W' : 'E'
                            }
                            break
                        case 'S':
                            if (movement === 'A') {
                                valid = rover.y - 1 >= 0
                                valid && rover.y--
                            } else {
                                rover.orientation = movement === 'L' ? 'E' : 'W'
                            }
                            break
                        case 'E':
                            if (movement === 'A') {
                                valid = rover.x + 1 <= this.robot.width
                                valid && rover.x++
                            } else {
                                rover.orientation = movement === 'L' ? 'N' : 'S'
                            }
                            break
                        case 'W':
                            if (movement === 'A') {
                                valid = rover.x - 1 >= 0
                                valid && rover.x--
                            } else {
                                rover.orientation = movement === 'L' ? 'S' : 'N'
                            }
                            break
                        default:
                            break
                    }
                    if (!valid) {
                        break
                    }
                }
                console.log(`${valid}, ${rover.orientation}, (${rover.x},${rover.y}).`)
            }
        }
    }
</script>