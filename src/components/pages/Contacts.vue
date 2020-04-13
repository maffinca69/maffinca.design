<template>
    <div class="contacts">
        <div class="content">
            <div class="logo">
                <div ref="text">/maffinca</div>
            </div>
        </div>
        <div class="divider"></div>
    </div>
</template>

<script>
    import {gsap} from 'gsap'
    import ScrollMagic from "scrollmagic"
    import scrollify from "jquery-scrollify";

    export default {
        name: "Contacts",
        data: () => ({
            isLoaded: false,
        }),
        mounted() {
            new ScrollMagic.Scene({triggerElement: 'footer'})
                .addTo(new ScrollMagic.Controller())
                .on('enter', () => {
                    if (this.isLoaded) return;
                    this.lineAnimation();
                });

               scrollify({
                    section:".page", // селектор для секций (разделов) на странице
                    scrollSpeed: 50,
                    offset : 0, // расстояние в пикселях для комппенсации положения каждого раздела.
                    scrollbars: false //Будет ли видна полоса прокрутки
                });

        },
        methods: {
            lineAnimation() {
                this.isLoaded = true;
                let tl = gsap.timeline();
                tl.set('.content', {alpha: 0});
                tl.set('.divider', {'margin-bottom': this.$refs.text.clientHeight / 1.5})

                tl.to(".divider", 1, {
                    width: '100vw', delay: 0.2, marginLeft: 0, onComplete: () => {
                        tl.to('.divider', {display: 'none', alpha: 0, onComplete: () => {
                                tl.to('.content', {alpha: 1})
                            }
                        })
                    }
                });
            }
        }
    }
</script>

<style scoped>
    .divider {
        height: 1px;
        background-color: white;
        text-align: center;
        width: 0;
        margin-left: 50%;
    }

    .contacts {
        font-family: 'Open Sans', serif;
        font-size: 2em;
    }
</style>
