<template>
    <div id="app">
        <div class="full_page_container">
            <div class="page" id="preview">
                <Preview/>
            </div>
            <div class="page" id="contacts">
                <Contacts/>
            </div>
        </div>
    </div>
</template>

<script>
    import Preview from "./components/pages/Preview";
    import Contacts from "./components/pages/Contacts";
    export default {
        name: 'App',
        components: {
            Preview,
            Contacts
        }
    }
</script>

<style>
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
        scroll-behavior: smooth;
    }

    ::-webkit-scrollbar {
        display: none;
    }

    .full_page_container {
        position: relative;
        overflow: hidden;
    }

    .page {
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100vh;
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

    @media only screen and (max-width: 768px) {
        .typed-cursor {
            height: 31px;
            border-left: .19em solid orange; /* The typwriter cursor */
        }
        .page {
            height: calc(100vh - 60px);
        }
    }
</style>
