<template>
    <main id="app">
        <Header/>
        <section id="container">
            <ActiveTab/>
        </section>
        <Footer/>
    </main>
</template>

<script>

    import Footer from "./components/Footer";
    import Header from "./components/Header";
    import ActiveTab from "./components/ActiveTab";

    export default {
        name: 'app',
        components: {
            ActiveTab,
            Header,
            Footer,
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

    #container {
        width: 80%;
        max-width: 900px;
        min-width: 320px;
        padding: 15px;
        background-color: #ffffff;
        margin: 0 auto;
    }

</style>