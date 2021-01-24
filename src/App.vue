<template>
  <div id="app">
    <div id="pages" class="container">
      <div class="section preview" data-anchor="main">
        <div class="typed_wrap">
          <h1 class="typed"></h1>
        </div>
        <footer>
          <a class="arrow" href="#contacts" style="opacity: 0; display: none">
            <img alt="Arrow Down Icon"
                 src="https://raw.githubusercontent.com/solodev/scroll-down-anchor/master/images/arrow-down-1.png">
          </a>
        </footer>
      </div>
      <div class="section contacts" data-anchor="contacts">
        <div ref="text" class="contact__slash"><a href="tg://resolve?domain=maffinca69">/maffinca</a></div>
        <div class="divider"></div>
      </div>
    </div>
  </div>
</template>

<script>
import Typed from 'typed.js';
import {gsap} from "gsap";

import fullpage from 'fullpage.js';

export default {
  name: 'App',
  data: () => ({
    contactViewed: false,
    lineWidth: 0,
    visibleLinks: false,
  }),
  mounted() {
    let context = this;
    console.error = function(){}
    new fullpage('#pages', {
      verticalCentered:true,
      sectionsColor: ['#1B1B1B', '#1B1B1B'],
      anchors:['main', 'contacts'],
      onLeave: function (origin) {
        if (origin.anchor === 'main' && !context.contactViewed) {
          setTimeout(() => {
            context.dividerAnimation()
          }, 500)
        }

      },
    });

    this.typed();
  },
  methods: {
    typed() {
      let options = {
        strings: ['Backend Developer', 'Jolly Joy', 'Maffinca69'],
        backSpeed: 35,
        typeSpeed: 45,
        onComplete: () => {
          let tl = gsap.timeline();
          tl.to(".arrow", 0.5, {autoAlpha: 1, display: 'block'});
        },
      };

      new Typed('.typed', options);
    },
    dividerAnimation() {
      let tl = gsap.timeline();
      tl.set('.contact__slash', {alpha: 0});
      tl.set('.divider', {'margin-bottom': this.$refs.text.clientHeight / 1.5})

      tl.to(".divider", 1, {
        width: '100vw', delay: 0.2,  onComplete: () => {
          tl.to('.divider', {display: 'none', alpha: 0, onComplete: () => {
              tl.to('.contact__slash', 1, {display: 'block', alpha: 1})
              this.contactViewed = true;
            }
          })
        }
      });
    }
  }
}
</script>

<style type="scss">
@font-face {
  src: url("assets/fonts/RobotoMono-Medium.ttf");
  font-family: "Open Sans";
}

html, body {
  background-color: #1B1B1B;
  margin: 0;
  padding: 0;
  text-rendering: optimizeLegibility;
  color: white;
}

.fp-tableCell {
  display: flex;
  align-items: center;
  justify-content: center;
}

.section {
  font-family: 'Open Sans', serif;
  font-size: 2em;

  text-align:center;
}

.typed-cursor {
  font-size: 1em;
  color: transparent;
  position: absolute;
  margin-top: 1.8em;
  height: 58px;
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  border-left: .15em solid orange; /* The typwriter cursor */
  margin-left: 3px;
}

a {
  text-decoration: none;
  color: white;
  transition-duration: 300ms;
}

a:hover {
  color: orange;
}

.typed_wrap {
  max-height: 132px;
}

.typed {
  display: inline-block;
}

footer {
  position: absolute;
  left: 0;
  bottom: 100vh;
  width: 100%;
  height: 80px;
}

.contact__slash {
  display: none;
}

.divider {
  height: 1px;
  background-color: white;
}

@media only screen and (max-width: 768px) {
  .preview {
    font-size: 1em;
  }

  .typed_wrap {
    height: 75px;
  }
}

@media only screen and (max-width: 768px) {
  .typed-cursor {
    height: 31px;
    border-left: .19em solid orange; /* The typwriter cursor */
  }
}
</style>
