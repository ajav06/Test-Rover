<template>
  <div id="app">
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
  </div>
</template>

<script>
import Field from './components/Field.vue'

export default {
  name: 'App',
  components: {
    Field
  }
}
</script>

