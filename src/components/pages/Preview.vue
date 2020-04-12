<template>
    <div class="preview">
        <div class="typed_wrap" ref="typedWrap">
            <h1 class="typed"></h1>
        </div>
        <div class="links" v-bind:style="{ 'visibility': visibleLinks ? 'visible' : 'hidden' }">
            <div class="line" v-bind:style="{ 'width': lineWidth + 'px' }"></div>
            <div class="lowerWrap">
                <div class="lower"><a href="tg://resolve?domain=maffinca69">Telegram</a></div>
            </div>
        </div>
        <footer>
            <a class="arrow" href="#contacts" style="opacity: 0">
                <img alt="Arrow Down Icon"
                     src="https://raw.githubusercontent.com/solodev/scroll-down-anchor/master/images/arrow-down-1.png">
            </a>
        </footer>
    </div>
</template>

<script>
    import Typed from 'typed.js';
    import {gsap} from "gsap";

    export default {
        name: "Preview",
        data: () => ({
            lineWidth: 0,
            visibleLinks: false,
        }),
        mounted() {
            this.typed()
        },
        methods: {
            typed() {
                let options = {
                    strings: ['Backend Developer', 'Jolly Joy', 'Maffinca69'],
                    backSpeed: 35,
                    typeSpeed: 45,
                    onComplete: () => {
                        let tl = gsap.timeline();
                        let width = this.$refs.typedWrap.clientWidth;
                        this.visibleLinks = true;
                        tl.set('.line', {'margin-left': width + 'px'});

                        tl.to(".line",1,{width: width, delay: 0.2, marginLeft:0});
                        tl.from(".lower", {duration: 0.75, y: -50}, "text");
                        tl.to(".arrow", 0.5, {autoAlpha: 1});
                    },
                };

                new Typed('.typed', options);
            }
        }
    }
</script>

<style scoped>
    .preview {
        font-family: 'Open Sans', serif;
        font-size: 2em;
        overflow: hidden;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        text-align: center;
    }

    .typed_wrap {
        max-height: 132px;
    }

    .typed {
        display: inline-block;
    }

    .line {
        height: 2px;
        background-color: white;
        text-align:center;
        width:0;
    }

    .lowerWrap {
        overflow: hidden;
        line-height: 52px;
    }

    footer {
        position: absolute;
        left: 0;
        bottom: 100vh;
        width: 100%;
        height: 80px;
    }

    @media only screen and (max-width: 768px) {
        .preview {
            font-size: 1em;
        }

        .typed_wrap {
            height: 75px;
        }
    }

</style>
