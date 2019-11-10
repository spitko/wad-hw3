<template>
    <main id="app">
        <header>
            <strong>Welcome to your dashboard!</strong>
        </header>
        <section id="container">
            <section id="main">
                <div class="content">
                    <component v-bind:is="selected" class="tab active"></component>
                </div>
                <div class="controls">
                    <button v-for="tab in tabs"
                            v-bind:key="tab"
                            v-bind:class="['pill', { active: selected === tab }]"
                            v-on:click="selected = tab">
                        {{ tab }}
                    </button>
                </div>
            </section>
        </section>
        <Links/>
    </main>
</template>

<script>

    import Profile from "./components/Profile";
    import Courses from "./components/Courses";
    import Links from "./components/Links";

    export default {
        data: function () {
            return {
                selected: "Profile",
                tabs: ["Profile", "Courses"]
            };
        },
        name: 'app',
        components: {
            Courses,
            Profile,
            Links
        }
    }
</script>
<style>
    * {
        box-sizing: border-box;
        font-family: 'Livvic', sans-serif;
    }

    html, body {
        padding: 0;
        margin: 0;
        width: 100%;
        height: 100%;
        background-color: #eaeaea;
    }

    main {
        position: relative;
        min-height: 100%;
        padding-bottom: 110px;
    }

    header {
        padding: 20px;
        background-color: #2196F3;
        color: #ffffff;
        text-align: center;
        margin-bottom: 10px;
        height: 60px;
    }

    #container {
        width: 80%;
        max-width: 900px;
        min-width: 320px;
        padding: 15px;
        background-color: #ffffff;
        margin: 0 auto;
    }

    .content {
        padding: 10px;
        border: 1px solid #cbcbcb;
    }

    .content .tab {
        display: none;
    }

    .content .tab.active {
        display: block;
    }

    .controls .pill {
        border: 1px solid #cbcbcb;
        background-color: #eaeaea;
        padding: 10px;
        border-bottom-left-radius: 4px;
        border-bottom-right-radius: 4px;
        border-top: none;
        margin-top: -1px;
        outline: none !important;
    }

    .controls .pill.active {
        background-color: #ffffff;
        border-top: 1px solid #ffffff;
    }

    .controls .pill:hover {
        cursor: pointer;
    }
</style>
