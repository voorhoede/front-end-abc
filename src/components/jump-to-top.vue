<template>
  <div class="jump-to-top">
    <a @click.prevent="animateScrollToElement('#top')" href="#top" class="jump-to-top__button">
      <arrow-icon class="jump-to-top__icon" />
      <span class="a11y-sr-only">Jump to navigation</span>
    </a>
  </div>
</template>

<script>
import animateScrollToElement from '../lib/animate-scroll-to-element'
import ArrowIcon from '../static/icons/arrow.svg'

export default {
  components: { ArrowIcon },
  methods: {
    animateScrollToElement
  }
}
</script>

<style>
@import '../assets/variables.css';

.jump-to-top {
  border-bottom: 1px solid var(--grey-medium);
}

.jump-to-top__button {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  padding: 0;
  width: 2rem;
  height: 2rem;
  transform: translateY(50%);
  background: var(--grey-light);
  border: 1px solid var(--grey-medium);
  border-radius: 50%;
  transition: border-color .15s linear;
}

.jump-to-top__icon {
  width: 1rem;
  height: 1.1rem;
  fill: var(--grey-medium--highlight);
  transition: fill .15s linear;
}

.jump-to-top__button:hover,
.jump-to-top__button:focus {
  outline: none;
  border-color: var(--grey-dark);
}

.jump-to-top__button:hover .jump-to-top__icon,
.jump-to-top__button:focus .jump-to-top__icon {
  animation: bounce-arrow .25s ease-in-out;
  transition: fill .15s linear;
  fill: var(--grey-dark);
}

@keyframes bounce-arrow {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-2px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>