<template>
    <div id="courses">
        <h1 class="title">Courses</h1>
        <table id="coursesTable">
            <thead>
            <tr>
                <th>#</th>
                <th>Course Title</th>
                <th>Semester</th>
                <th>Grade</th>
            </tr>
            </thead>
            <tbody>

            <tr v-for="(course, index) in courseArr" :key="course.id">
                <td>{{index}}</td>
                <td>{{course.title}}</td>
                <td>{{course.semester}}</td>
                <td>{{course.grade}}</td>
            </tr>
            <!--<tr>
                <td>1</td>
                <td>Agile software development</td>
                <td>1</td>
                <td>82</td>
            </tr>
            <tr>
                <td>2</td>
                <td>System modeling</td>
                <td>1</td>
                <td>85</td>
            </tr>
            <tr>
                <td>3</td>
                <td>Object-oriented programming</td>
                <td>2</td>
                <td>99</td>
            </tr>
            <tr>
                <td>4</td>
                <td>Estonian language Level A2</td>
                <td>2</td>
                <td>65</td>
            </tr>-->
            </tbody>
        </table>
        <br>
        <br>
        <AddCourse/>
    </div>
</template>

<script>
    import AddCourse from "./AddCourse";
    import Course from "../models/Course";
    import {bus} from "../main"

    export default {
        name: 'Courses',

        data: () => {
            return {
                showForm: false
            }
        },
        components: {
            AddCourse,
        },
        methods: {
            saveCourseMethod: function (title, semester, grade) {
                this.courseArr.push(new Course(title, semester, grade));
                bus.$emit("gpaChange", this.getGpa())
            },
            getGpa: function () {
                let sum = 0;
                this.courseArr.forEach(function (element) {
                    switch (true) {
                        case element.grade > 90:
                            sum += 4;
                            break;
                        case element.grade > 80:
                            sum += 3;
                            break;
                        case element.grade > 70:
                            sum += 2;
                            break;
                        case element.grade > 60:
                            sum += 1;
                            break;
                        case element.grade > 50:
                            sum += 0.5;
                            break;
                    }
                });
                return sum / this.courseArr.length
            }

        },
        created() {
            const vm = this;
            bus.$on('saveCourse', function (event) {
                vm.saveCourseMethod(event[0], event[1], event[2]);
            });
        },
        props: {
            courseArr: Array
        }
    }
</script>

<style scoped>

    table {
        width: 100%;
        border-collapse: collapse;

    }

    table th {
        padding: 8px 12px;
        text-align: left;
        border: 1px solid #cbcbcb;
        background-color: #162b4e;
        color: #ffffff;
    }

    table td {
        padding: 8px 12px;
        border: 1px solid #cbcbcb;
    }

</style>