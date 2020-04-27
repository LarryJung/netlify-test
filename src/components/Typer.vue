<template>
  <div>
    <div>
      <span class="type-animation animating">Excellentasdflsadkfjalsdkfjlaskdjf</span>Website
    </div>
  </div>
</template>

<script>
// Not required for animation, just provides "Retype" button functionality

// Animation restart method from CSS-Tricks:
// @link https://css-tricks.com/restart-css-animation/

// const button = document.querySelector("button");
// const word = document.querySelector("h1 span");

// // reset the transition by...
// button.addEventListener(
// 	"click",
// 	function (e) {
// 		e.preventDefault;

// 		// -> removing the class
// 		word.classList.remove("animating");

// 		// -> triggering reflow /* The actual magic */
// 		void word.offsetWidth;

// 		// -> and re-adding the class
// 		word.classList.add("animating");
// 	},
// 	false
// );

export default {

};
</script>

<style lang="scss">
// Learn more:
// @link https://dev.to/5t3ph/pure-css-typing-animation-1nld

// "Type" width
// - controls how much the word container expands when each letter is "typed"
// - will need adjusted depending on word and typeface
$chWidth: 0.49em;
// Word length
$chCount: 35;
// Typing animation length
$typeDuration: 180ms * $chCount;

$color: slateblue;
$bg: #f7f3ff;
$cursor: scale-color($color, $lightness: -60%);

// body {
//   display: grid;
//   place-items: center;
//   min-height: 100vh;
//   background-color: $bg;
//   color: $color;
//   font-family: Rosario, sans-serif;
// }

// h1 {
//   font-size: 4.5rem;
//   text-align: center;
// }

.type-animation {
  display: inline-flex;
  width: 0;
  overflow: hidden;
  padding-right: 0.08em;
  position: relative;

  &:after {
    content: "";
    // background: $bg;
    position: absolute;
    right: 0;
    top: -0.05em;
    bottom: -0.05em;
    width: 0.08em;
    border-right: 2px solid transparent;
  }

  &.animating {
    animation: type $typeDuration;
    animation-fill-mode: forwards;
    animation-delay: 1s;

    &:after {
      $cursorLoopCount: ((($chCount + 1) * 180)/320) + 3;
      animation: cursor 320ms $cursorLoopCount ease-in-out;
    }
  }
}

@keyframes cursor {
  0%,
  100% {
    border-color: $bg;
  }
  50% {
    border-color: $cursor;
  }
  100% {
    width: 0;
  }
}

$frameSize: 100 / $chCount;
@keyframes type {
  @for $ch from 1 to $chCount {
    $frame: $ch * $frameSize;
    #{$frame}% {
      width: $ch * $chWidth;
    }
  }
  100% {
    width: ($chCount - 1) * $chWidth;
    padding-right: 0;
  }
}
</style>