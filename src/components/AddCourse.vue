<template>
    <div>
        <button @click="showForm = !showForm" id="add-course-button" class="blue-button">+</button>
        <span v-if="showForm" id="add-course">
            <input class="input" v-model="title" type="text" placeholder="Course title" id="title">
            <input class="input" v-model.number="semester" type="number" min="1" max="8" placeholder="Semester"
                   id="semester">
            <input class="input" v-model.number="grade" type="number" min="0" max="100" placeholder="Grade" id="grade">
            <button class="green-button" @click="saveCourse" id="save-course">Save</button>
            <button class="grey-button" @click="cancelCourse" id="cancel-course">Cancel</button>
        </span>
    </div>
</template>

<script>
    import {bus} from "../main"

    export default {
        name: 'AddCourse',
        data: function () {
            return {
                grade: '',
                semester: '',
                title: '',
                showForm: false

            };
        },
        methods: {
            saveCourse: function () {
                bus.$emit("saveCourse", [this.title, this.semester, this.grade]);
                this.clearFields();
            },
            clearFields: function () {
                this.grade = '';
                this.semester = '';
                this.title = '';
                this.showForm = false;
            },
            cancelCourse: function () {
                this.showForm = false
                this.clearFields()
            }
        }

    }


</script>

<style scoped>
    .blue-button {
        background-color: #162b4e;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }

    .green-button {
        background-color: #69f378;
        color: #ffffff;
        border: none;
        padding: 10px 10px;
    }

    .grey-button {
        background-color: #e1e8e6;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }

    .grey-button:hover {
        background-color: crimson;
    }

    .input {
        border: 1px solid #cccccc;
        padding: 10px 20px;
        min-width: 135px;
    }
</style>
