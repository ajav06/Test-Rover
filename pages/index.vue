<template>
    <section class="hero is-light is-bold is-fullheight">

        <div class="hero-body">
            <div class="container">
                <h2 class="title is-2 has-text-centered">
                    Rover
                </h2>

                <Field />
            </div>
        </div>

    </section>
</template>

<script>
    import Field from '../components/Field'
    export default {
        components: {
            Field
        }

    }
</script>