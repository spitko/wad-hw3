<template>
    <div id="profile">
        <div class="avatar">
            <img src="../assets/john.jpg" id="picture" alt="My picture">
        </div>
        <div class="info">
            <ul>
                <li id="name">{{user.firstname + " " + user.lastname}}</li>
                <li id="birthdate">{{formatDate(user.birthdate)}}</li>
                <li id="faculty">{{user.faculty}}</li>
            </ul>
        </div>
        <div id="gpa">
            <strong :key="gpaKey">{{user.gpa}}</strong>
        </div>
        <div class="clear-fix"></div>
    </div>
</template>
<script>
    import User from "../models/User";
    import {bus} from "../main";

    export default {
        name: 'Profile',
        data: () => {
            return {
                gpaKey: 0,
            }
        },
        created() {
            const vm = this;
            bus.$on("gpaChange", function (event) {
                vm.user.gpa = event;
                vm.gpaKey += 1;
            })
        },
        methods: {
            formatDate: function formatDate(date) {
                let d = new Date(date),
                    month = '' + (d.getMonth() + 1),
                    day = '' + d.getDate(),
                    year = d.getFullYear();

                if (month.length < 2)
                    month = '0' + month;
                if (day.length < 2)
                    day = '0' + day;

                return [year, month, day].join('/');
            }
        },
        props: {
            user: User
        }
    }
</script>


<style>

    .clear-fix {
        clear: both;
    }

    #profile {
        border-bottom: 1px dashed #a7a7a7;
        padding-bottom: 10px;
        margin-bottom: 10px;
    }

    #profile div:not(.clear-fix) {
        height: 190px;
        float: left;
        position: relative;
    }

    #profile .avatar {
        width: 35%;
        text-align: center;
    }

    #profile .avatar img {
        width: 180px;
        border-radius: 50%;
        height: 180px;
    }

    #profile .info {
        width: 45%;
    }

    #profile #gpa {
        width: 20%;
    }

    #profile #gpa strong {
        position: absolute;
        width: 100%;
        height: 60px;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        margin: auto auto;
        font-size: 60px;
        line-height: 60px;
        text-align: center;
    }

</style>