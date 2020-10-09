<template>
    <div>
        <b-field class="has-text-centered">
            <b-button type="is-info">Init Test</b-button>
        </b-field>
    </div>
</template>

<script>
    export default {
        name: 'Output',
        props: {
            robot: Object
        },
        methods: {
            removeWhiteSpace(s) {
                return s.replace(/\s+/g, '').trim();
            },

            validateCommands(width, height, orientation, coordinates, movements) {
                if (!width || !height || !orientation || !coordinates || !movements) {
                    return 'Error -> Please enter all data'
                }
                let rover = {
                    orientation: removeWhiteSpace(orientation).toUpperCase(),
                    x: Number(removeWhiteSpace(coordinates).split(',')[0]),
                    y: Number(removeWhiteSpace(coordinates).split(',')[1])
                }
                const array = removeWhiteSpace(movements.toUpperCase()).split('')
                let valid = true
                for (let i = 0; i < array.length; i++) {
                    const movement = array[i]
                    switch (rover.orientation) {
                        case 'N':
                            if (movement === 'A') {
                                valid = rover.y + 1 <= height
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
                                valid = rover.x + 1 <= width
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
                return `${valid}, ${rover.orientation}, (${rover.x},${rover.y}).`
            }
        }
    }
</script>