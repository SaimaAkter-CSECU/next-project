<template>
    <v-app app color="transparent">
        <Header />
        <v-main>
            <Banner />
            <Category />
            <Events />
            <UpcommingEvents />
            <Featured />
            <Footer />
            <BackToTop />
        </v-main>
    </v-app>
</template>

<script>
    import Header from './Header';
    import Banner from './Banner';
    import Category from './Category';
    import Featured from './Featured';
    import Events from './Events';
    import UpcommingEvents from './UpcommingEvents';
    import Footer from './Footer'; 
    import BackToTop from './BackToTop';
    export default {
        name: 'Home', 
        components: {
            Header, Banner, Footer, Featured, Category, Events, UpcommingEvents, BackToTop
        }
    }
</script>