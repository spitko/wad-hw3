<template>
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
</template>

<script>
    import Profile from "./Profile";
    import Courses from "./Courses";

    export default {
        name: "ActiveTab",
        data: function () {
            return {
                selected: "Profile",
                tabs: ["Profile", "Courses"]
            };
        },
        components: {
            Profile,
            Courses
        }
    }
</script>

<style scoped>

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