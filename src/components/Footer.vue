<template>
    <v-footer id="footer" class="white--text">
        <v-container>
            <v-row>
                <v-col
                    cols="12"
                    sm="12"
                    md="3"
                >
                    <v-img
                        :src="footerLogo"
                        max-height="300"
                        width= "250"
                        max-width="90%"
                    ></v-img>
                    <p class="my-5">
                        Youth Opportunities is the largest opportunities discovery platform for youth across the globe.
                    </p>
                    <p>
                        <small>
                            <router-link to="/HelloWorld">Terms and Policy</router-link>
                        </small>
                    </p>
                    <p class="my-3">&copy; 2021 Youth Opportunities</p>
                </v-col>
                <v-col
                    col="12"
                    sm="12"
                    md="3"
                >
                    <v-list class="white--text" style="background-color: transparent;">
                        <v-list-item-title> 
                            <h5 class="footer-list-title pt-3 pb-4 pl-4 font-weight-thin">Youth Opportunities</h5> 
                        </v-list-item-title>
                        <v-list-item v-for="youthListItem in yuothListItems" :key="youthListItem.title">
                            <v-list-item-title>
                                <router-link :to="youthListItem.path">{{youthListItem.title}}</router-link>
                            </v-list-item-title>
                        </v-list-item>
                    </v-list>
                </v-col>
                <v-col
                    cols="12"
                    sm="12"
                    md="3"
                >
                    <v-list class="white--text contact" color="transparent">
                        <v-list-item-title> 
                            <h5 class="footer-list-title pt-3 pb-4 pl-4 font-weight-thin">Contact</h5> 
                        </v-list-item-title>
                        <v-list-item v-for="contactListItem in contactListItems" :key="contactListItem.title">
                            <v-list-item-title>
                                <router-link :to="contactListItem.path">{{contactListItem.title}}</router-link>
                            </v-list-item-title>
                        </v-list-item>
                    </v-list>
                </v-col>
                <v-col
                    cols="12"
                    sm="12"
                    md="3"
                >
                    <v-list class="white--text" color="transparent">
                        <v-list-item-title> 
                            <h5 class="mt-3 mb-4 pl-4 font-weight-thin">Keep Connected</h5> 
                        </v-list-item-title>
                        <v-list-item-content class="flex-column">
                            <v-row>
                                <v-col
                                    cols="12"
                                    xs="12"
                                >
                                    <div class="my-3 px-3 social-icons">
                                        <a href="#" class="mx-1">
                                            <v-icon
                                                large
                                                >
                                                mdi-facebook 
                                            </v-icon>
                                        </a>
                                        <a href="#" class="mx-1">
                                            <v-icon
                                                large
                                                >
                                                mdi-linkedin 
                                            </v-icon>
                                        </a>
                                        <a href="#" class="mx-1">
                                            <v-icon
                                                large
                                                >
                                                mdi-whatsapp 
                                            </v-icon>
                                        </a>
                                        <a href="#" class="mx-1">
                                            <v-icon
                                                large
                                                >
                                                mdi-youtube 
                                            </v-icon>
                                        </a>
                                        <a href="#" class="mx-1">
                                            <v-icon
                                                large
                                                >
                                                mdi-instagram 
                                            </v-icon>
                                        </a>
                                    </div>
                                </v-col>
                            </v-row>
                            <v-row>
                                <v-col
                                    cols="12"
                                    xs="12"
                                >
                                    <div class="d-flex justify-space-around" justify="space-around">
                                            <a href="#" class="mr-1" >
                                                <v-img
                                                    :src="gPlay"
                                                    max-width="100%"
                                                    rounded
                                                >
                                                </v-img>
                                            </a>
                                            <a href="#" >
                                                <v-img
                                                    :src="iPlay"
                                                    max-width="100%"
                                                    rounded
                                                >
                                                </v-img>
                                            </a>
                                    </div>
                                </v-col>
                            </v-row>
                        </v-list-item-content>
                    </v-list>
                </v-col>
            </v-row>
        </v-container>
    </v-footer>
</template>

<script>
    import footerLogo from '../assets/image/next-opp-logo-white.png';
    import gPlay from '../assets/image/g-play.png';
    import iPlay from '../assets/image/i-play.png';
    export default {
        name: 'Footer', 
        data: () => ({
            footerLogo: footerLogo,
            gPlay: gPlay,
            iPlay: iPlay,
            yuothListItems :[
                {
                    title: 'About',
                    path: '/InfoPage', 
                },
                {
                    title: 'Partners',
                    path: '/About/Partners', 
                },
                {
                    title: 'FAQs',
                    path: '/About/FAQs', 
                },
                {
                    title: 'Join',
                    path: '/About/Join', 
                },
                {
                    title: 'Local Network',
                    path: '/About/Local', 
                },
            ],
            contactListItems :[
                {
                    title: 'Press',
                    path: '/About/Press', 
                },
                {
                    title: 'Promote Program',
                    path: '/About/Promote', 
                },
                {
                    title: 'Contact',
                    path: '/About/Contact', 
                },
            ],
        }), 
    }
</script>