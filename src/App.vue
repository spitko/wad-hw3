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
        <footer>
            <ul class="links">
                <li>
                    <a href="https://ois2.ut.ee/" target="_blank">OIS</a>
                </li>
                <li>
                    <a href="https://courses.cs.ut.ee/" target="_blank">Courses</a>
                </li>
            </ul>
        </footer>
    </main>
</template>

<script>

    import Profile from "./components/Profile";
    import Courses from "./components/Courses";
    // eslint-disable-next-line no-unused-vars
    import Course from "./models/Course";
    // eslint-disable-next-line no-unused-vars
    import User from "./models/User";

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
            Profile
        }
    }
</script>

