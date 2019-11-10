<template>
    <section id="main">
        <div class="content">
            <Profile v-if="selected === 'Profile'" v-bind:user="user"/>
            <Courses v-if="selected === 'Courses'" v-bind:course-arr="courseArr"/>
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
    import Course from "../models/Course";
    import User from "../models/User";

    export default {
        name: "ActiveTab",
        data: function () {
            return {
                courseArr: [
                    new Course('Agile software development', 1, 82),
                    new Course('System modeling', 2, 99),
                    new Course('Object-oriented programming', 2, 99),
                    new Course('Estonian language Level A2', 2, 65)
                ],
                user: new User('John', 'Doe', new Date('11/10/1990'), 'Software Engineering', 2.75),
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