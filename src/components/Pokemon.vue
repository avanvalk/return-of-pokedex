
<template>
<transition-group 
  name="staggered-transition"
  v-on:before-enter="beforeEnter"
  v-on:enter="enter"
  v-on:leave="leave"
>
  <li
  v-bind:key="pokemon"
  >
    <img v-bind:src="pokemon.url_image"/>
    <div class="info">
      <h3>{{ pokemon.pokemon }}</h3>
      <p>attack: {{ pokemon.attack }}</p>
      <p>defense: {{ pokemon.defense }}</p>
      <p>health: {{ pokemon.hp }}</p>
    </div>
  </li>
</transition-group>
</template>

<script>

export default {
  props: {
    pokemon: Object
  },
  methods: {
    beforeEnter: function(el) {
      el.style.opacity = 0;
      el.style.height = 0;
    },
    enter: function(el, done) {
      var delay = el.dataset.index * 150;
      setTimeout(function() {
        Velocity(
          el,
          { opacity: 1, height: '1.6em' },
          { complete: done }
        );
      }, delay);
    },
    leave: function(el, done) {
      var delay = el.dataset.index * 150;
      setTimeout(function() {
        Velocity(
          el,
          { opacity: 0, height: 0 },
          { complete: done }
        );
      }, delay);
    }
  }
};



</script>

<style scoped>
li {
  position: relative;
  height: 300px;
}
img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  object-fit: cover;
}
.info {
  position: absolute;
  bottom: 0;
  width: 100%;
  background: rgba(255, 255, 255, 0.8);
  text-align: center;
}
h3, p {
  margin: 0;
}
</style>