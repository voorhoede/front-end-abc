<template>
  <nav id="top" class="navigation" role="navigation">
    <ul class="flat-list">
      <li class="navigation__item" v-for="concept in concepts" :key="concept.slug">
        <a @click.prevent="animateScrollToElement('#' + concept.slug)" :href="'#' + concept.slug">
          <concept-icon :backgroundColor="concept.color" :imageUrl="concept.icon" />
          <span class="navigation__content">{{ concept.name }}</span>
        </a>
      </li>
    </ul>
  </nav>
</template>

<script>
import animateScrollToElement from '../lib/animate-scroll-to-element'
import ConceptIcon from '../components/concept-icon'

export default {
  components: { ConceptIcon },
  props: {
    concepts: {
      type: Array,
      required: true
    },
  },
  methods: {
    animateScrollToElement
  }
}
</script>

<style>
@import '../assets/variables.css';

.navigation {
  min-height: 35%;
  background-color: var(--grey-light);
  width: 100%;
  padding: calc(var(--spacing-default) * 3) var(--spacing-double);
}


@media (min-width: 768px) {
  .navigation {
    height: 30vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}

.navigation ul {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 100%;
  max-width: 600px;
  margin: 0;
}

.navigation__item {
  flex: 0 0 40%;
  margin: 0 var(--spacing-half) var(--spacing-default) var(--spacing-half);
}

@media (min-width: 400px) {
  .navigation__item {
    flex: 0 0 20%;
  }
}

.navigation__item a {
  display: block;
  background: none;
  font-size: var(--font-size-smaller);
  text-align: center;
  line-height: 1.4;
  border: none;
}

.navigation__content,
.navigation__content {
  border-bottom: 1px solid transparent;
}

.navigation__item a:hover .navigation__content,
.navigation__item a:focus .navigation__content {
  border-bottom: 1px solid var(--grey-dark);
}

.navigation .concept-icon {
  flex: 0 0 auto;
  margin: 0 auto var(--spacing-half) auto;
  width: 3rem;
  height: 3rem;
}
</style>
