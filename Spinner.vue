<template>
<svg class="spinner" width="24" height="24" viewBox="25 25 50 50">
  <circle class="path" cx="50" cy="50" r="20" fill="none" stroke-width="4" stroke-miterlimit="10" />
</svg>
</template>

<style lang="scss" scoped>
.spinner {
  transform-origin: center center;
  animation: rotate 2s linear infinite;
}

.path {
  stroke-dasharray: 1, 200;
  stroke-dashoffset: 0;
  stroke-linecap: round;
  animation: dash 1.5s ease-in-out infinite, color 6s ease-in-out infinite;
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}

@keyframes dash {
  0% {
    stroke-dasharray: 1, 200;
    stroke-dashoffset: 0;
  }
  50% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -35px;
  }
  100% {
    stroke-dasharray: 89, 200;
    stroke-dashoffset: -124px;
  }
}

@keyframes color {
  100%,
  0% {
    stroke: #03a9f4;
  }
  40% {
    stroke: #03a9f4;
  }
  66% {
    stroke: #03a9f4;
  }
  80%,
  90% {
    stroke: #03a9f4;
  }
}
</style>
