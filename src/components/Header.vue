<template>
    <div>
        <v-app-bar
            fixed
            flat
            :color="bg"
            v-scroll="updateScroll"
            elevate-on-scroll
        >
            <v-container class="d-flex">
                <div class="d-flex align-center">
                    <v-img
                        alt="Logo"
                        class=""
                        contain
                        min-width="100"
                        :src="logo"
                        width="250px"
                        :height= "logoHeight"
                    />
                </div>

                <v-spacer></v-spacer>
                <div class="nav hidden-sm-and-down">
                    <v-menu 
                        bottom
                        transition="slide-x-transition"
                        close-delay="170"
                        offset-y 
                        class="browseBtn"
                        close-on-content-click
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-btn
                                text
                                tile
                                :color="menuColor"
                                v-bind="attrs"
                                v-on="on"
                            >
                                Browse Opportunity   
                                <v-icon class="ml-2">mdi-chevron-down</v-icon> 
                            </v-btn>
                        </template>
                        <v-list class="nav-list parent" >
                            <v-list-item
                                class="pr-0"
                                style="border-bottom: 1px solid rgba(255,255,255,0.6);"
                            >
                                <router-link to="/Browse">
                                    <v-list-item-title style="line-height: 47px;">Any Opportunity</v-list-item-title>
                                </router-link>
                            </v-list-item>
                            <div
                                v-for="opportunity in opportunities"
                                :key="opportunity.id"
                                class="main-list"
                            >
                                <v-list-item
                                    @click="opp(opportunity.id)"
                                    v-if="!opportunity.subList"
                                    class="pr-0"
                                >
                                    <v-list-item-title style="line-height: 47px;" >{{ opportunity.title }}</v-list-item-title>
                                </v-list-item>
                                <v-list-item
                                    @click="opp(opportunity.id)"
                                    v-else
                                    class="pr-0"
                                >
                                    <v-menu 
                                        open-on-hover
                                        offset-x 
                                        class="browseBtn"
                                    >
                                        <template v-slot:activator="{ on, attrs }">
                                            <v-list-item-title 
                                                v-bind="attrs"
                                                v-on="on"
                                                style="line-height: 47px;" 
                                                class="d-flex justify-space-between" 
                                            >
                                                {{ opportunity.title }}
                                                <v-icon class="mr-2 white--text" color="white">mdi-plus</v-icon> 
                                            </v-list-item-title>
                                        </template>
                                        <v-list class="child">
                                            <v-list-item
                                                v-for="subList in opportunity.subList"
                                                :key="subList.id"
                                                @click="opp(subList.id)"
                                            >
                                                <v-list-item-title style="line-height: 47px;"  >{{ subList.title }}</v-list-item-title>
                                            </v-list-item>
                                        </v-list>
                                    </v-menu>
                                </v-list-item>
                            </div>
                        </v-list>
                    </v-menu>
                    <v-btn
                        text
                        tile
                        :color="menuColor"
                    >
                        <router-link to="/post">
                            Post an Opportunity   
                        </router-link>
                    </v-btn>
                    <v-menu offset-y class="searchBtn">
                        <template v-slot:activator="{ on, attrs }">
                            <v-btn 
                                icon
                                tile
                                :color="menuColor"
                                v-bind="attrs"
                                v-on="on"
                                text
                            >
                                <v-icon>
                                    mdi-magnify
                                </v-icon>
                            </v-btn>
                        </template>
                        <div 
                            class="d-flex justify-between align-center pa-2 searchDiv"
                            @click.stop.prevent 
                        >
                                <v-autocomplete
                                    v-model="select"
                                    :loading="loading"
                                    :items="items"
                                    :search-input.sync="search"
                                    class="mx-3"
                                    flat
                                    hide-no-data
                                    hide-details
                                    placeholder="Start Typing to Search..."
                                    solo
                                ></v-autocomplete>
                                

                                <v-btn
                                    color="primary"
                                    @click="find()"
                                >
                                    Search
                                </v-btn>
                        </div>
                    </v-menu>
                </div>
                

                <v-app-bar-nav-icon 
                    :color="menuColor"
                    @click= "sideNavbar = !sideNavbar" 
                    class="hidden-md-and-up"
                >
                </v-app-bar-nav-icon>
            </v-container>
        </v-app-bar>
        <v-navigation-drawer 
            v-model="sideNavbar"
            absolute
            temporary
            width= "300"
            max-width= "90vw" 
            background-color= "white"
        >
            <v-list-item class="black--text">
                <v-list-item-content>
                    <v-list-item-title 
                        class="text-center d-grid justify-center mb-4"
                        width="100%"
                    >
                        <v-img
                            :src="logo2"
                            height="65"
                            width="61"
                            class="mx-auto"
                        >
                        </v-img>
                    </v-list-item-title>
                    
                    <v-list-item-title class="text-h6 text-center">
                        Nextive Solution
                    </v-list-item-title>
                </v-list-item-content>
            </v-list-item>

            <v-divider></v-divider>

            <v-list
                max-height="80vh"
                class="overflow-y-auto black--text"
                background-color="white"
                style="background-color: white !important"
            >
                <v-list-item>
                    <v-btn
                        text
                        tile
                    >
                        <router-link to="/Browse">
                            Browse Opportunity   
                        </router-link>
                    </v-btn>
                </v-list-item>
                <v-list-item>
                    <v-list class="ps-5 grey--text" style="background-color: white !important">
                        <div
                            v-for="opportunity in opportunities"
                            :key="opportunity.id"
                        >
                            <v-list-item
                                @click="opp(opportunity.id)"
                                class="pr-0"
                                style="border-bottom: 1px solid rgba(0,0,0,0.3);"
                            >
                                <v-list-item-title 
                                    style="color:#222;"
                                >
                                    {{ opportunity.title }}
                                </v-list-item-title>
                                
                            </v-list-item>
                            <v-list v-show="opportunity.subList" class="nav-list ps-5" style="background-color: white !important;">
                                <v-list-item
                                    v-for="subList in opportunity.subList"
                                    :key="subList.id"
                                    @click="opp(subList.id)"
                                >
                                    <v-list-item-title   
                                        style="border-bottom: 1px solid rgba(0,0,0,0.3); color:#222;"
                                    >
                                        {{ subList.title }}
                                    </v-list-item-title>
                                </v-list-item>
                            </v-list>
                        </div>
                    </v-list>
                </v-list-item>
                <v-list-item>
                    <v-btn
                        text
                        tile
                    >
                        <router-link to="/Post">
                            Post an Opportunity   
                        </router-link>
                    </v-btn>
                </v-list-item>
                <v-list-item>
                    <div 
                        class="pa-2"
                        @click.stop.prevent 
                    >
                        <v-autocomplete
                            v-model="select"
                            :loading="loading"
                            :items="items"
                            :search-input.sync="search"
                            class="mx-3"
                            flat
                            hide-no-data
                            hide-details
                            placeholder="Start Typing to Search..."
                            solo
                        ></v-autocomplete>
                        
                        <v-btn
                            color="primary"
                            @click="find()"
                        >
                            Search
                        </v-btn>
                    </div>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>

<script>
    import logo1 from '../assets/image/yo-logo-web.png'
    import logo2 from '../assets/image/yo_logo_icon.png'
    export default {
        name: 'Header', 
        data: () => ({
            logo: logo1, 
            logo2: logo2, 
            bg: 'transparent', 
            menuColor: 'white',
            logoHeight: "auto", 
            scrollPosition: null, 

            loading: false,
            items: [],
            search: null,
            select: null,
            posts: [
                'Alabama',
                'Alaska',
                'American Samoa',
                'Arizona',
                'Arkansas',
                'California',
                'Colorado',
                'Connecticut',
                'Delaware',
                'District of Columbia',
                'Federated States of Micronesia',
                'Florida',
                'Georgia',
                'Guam',
                'Hawaii',
                'Idaho',
                'Illinois',
                'Indiana',
                'Iowa',
                'Kansas',
                'Kentucky',
                'Louisiana',
                'Maine',
                'Marshall Islands',
                'Maryland',
                'Massachusetts',
                'Michigan',
                'Minnesota',
                'Mississippi',
                'Missouri',
                'Montana',
                'Nebraska',
                'Nevada',
                'New Hampshire',
                'New Jersey',
                'New Mexico',
                'New York',
                'North Carolina',
                'North Dakota',
                'Northern Mariana Islands',
                'Ohio',
                'Oklahoma',
                'Oregon',
                'Palau',
                'Pennsylvania',
                'Puerto Rico',
                'Rhode Island',
                'South Carolina',
                'South Dakota',
                'Tennessee',
                'Texas',
                'Utah',
                'Vermont',
                'Virgin Island',
                'Virginia',
                'Washington',
                'West Virginia',
                'Wisconsin',
                'Wyoming',
            ],
            opportunities: [
                {
                    id: 1, 
                    title: 'Deadline approaching', 
                },
                {
                    id: 2, 
                    title: 'SDG', 
                },
                {
                    id: 3, 
                    title: 'On Going', 
                },
                {
                    id: 4, 
                    title: 'Competitions', 
                    subList: [
                        {
                            id: 1, 
                            title: 'Awards',
                        },
                        {
                            id: 2, 
                            title: 'Grants',
                        }
                    ],
                },
                {
                    id: 5, 
                    title: 'Conference', 
                },
                {
                    id: 6, 
                    title: 'Scholarships', 
                    subList: [
                        {
                            id: 1, 
                            title: 'Masters/ Post graduate',
                        },
                        {
                            id: 2, 
                            title: 'PhD/ Doctoral',
                        }, 
                        {
                            id: 3, 
                            title: 'Summer School/ Winter School',
                        }, 
                        {
                            id: 4, 
                            title: 'Undergraduate',
                        }
                    ],
                },
                {
                    id: 7, 
                    title: 'Exchange Programs', 
                },
                {
                    id: 8, 
                    title: 'Fellowships', 
                },
                {
                    id: 9, 
                    title: 'Internships', 
                },
                {
                    id: 10, 
                    title: 'Workshops', 
                },
                {
                    id: 11, 
                    title: 'Miscellaneous', 
                },
            ],
            sideNavbar: false, 
        }),
        watch: {
            search (val) {
                val && val !== this.select && this.querySelections(val)
            },
        },
        methods: {
            updateScroll(){
                this.scrollPosition = window.scrollY; 
                if (this.scrollPosition > 80) {
                    this.bg = 'white';
                    this.logo = logo2; 
                    this.menuColor = '#757575'; 
                    this.logoHeight = "60px"; 
                }
                else{
                    this.bg = 'transparent';
                    this.logo = logo1; 
                    this.menuColor = 'white'; 
                    this.logoHeight = "60px"
                }
            }, 
            querySelections (v) {
                this.loading = true
                setTimeout(() => {
                this.items = this.posts.filter(e => {
                    return (e || '').toLowerCase().indexOf((v || '').toLowerCase()) > -1
                })
                this.loading = false
                }, 500)
            },
            async opp(i){
                localStorage.setItem("opportunity", i); 
                this.$router.push('/Browse'); 
            },
            async find(){
                console.log(this.select); 
                console.log(this.search); 
                localStorage.setItem("search", this.search); 
                this.$router.push('/Search'); 
            }
        },
        mounted() {
            this.updateScroll(); 
        }
    }
</script>

<style lang="scss" scoped>
    .v-app-bar{
        .v-image.v-responsive {
            .v-responsive__sizer{
                padding-bottom: 24.6787% !important;
                height: 60px; 
            }
            .v-image__image.v-image__image--contain{
                background-position: left center !important;
            }
            .v-responsive__content{
                width: 250px !important;
            }
        }
    }
    .theme--light.v-list {
        background: rgba(0,0,0,0.5) !important;
        color: rgb(255,255,255) !important;
        .v-list-item__title{
            color: white; 
        }
    }
    .v-autocomplete__content .theme--light.v-list {
        background: white !important;
        color: #222 !important;
        .v-list-item__title{
            color: #222; 
        }
    }
    .parent:hover > .child{
        display: block !important;
    }

</style>