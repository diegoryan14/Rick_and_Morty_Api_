<template>
    <div>
        <nav class="navbar navbar-dark bg-dark">
            <div class="container-fluid">
                <h5 class="text-center" style="color: white; margin-top: 10px;">Rick and Morty</h5>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarToggleExternalContent" aria-controls="navbarToggleExternalContent" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
            </div>
        </nav>
    </div>
    <div class="container texte-center">
        <div class="row">
            <div class="row col-12">
                <div class="container texte-center">
                    <div class="row">
                        <div v-if="validation == '1'" class="row col-12">
                            <div class="row col-12" style="margin-bottom: 10px; margin-top: 20px;">
                                <div class="row col-4"></div>
                                <div class="row col-4">
                                    <button @click="set_episodes()" type="button" class="btn btn-primary">Episode</button>
                                </div>
                                <div class="row col-4"></div>
                            </div>
                            <div v-for="x in api" style="margin-top: 5%;" class="col-6 mt-4 d-flex justify-content-center">
                                <div class="col-sm-12 col-md-8">
                                    <div id="card" style="background-color: white;" class="card">
                                        <div  class="card-body row">
                                            <div style="font-weight: bold; font-style: italic; font-family: 'Courier New', Courier, monospace;" class="text-center"><b>{{x.name}}</b></div>
                                            <div style="margin-top: 5%; margin-bottom: 5%;" class="text-center">
                                                <img :src="x.image" width="150">
                                            </div>
                                            <div style="margin-top: -20px; font-weight: bold; font-style: italic; font-family: 'Courier New', Courier, monospace;">
                                                <p class="mt-4"> <b>Location:</b> {{x.location.name}}</p>
                                            </div>
                                            <div style="margin-top: -20px; font-weight: bold; font-style: italic; font-family: 'Courier New', Courier, monospace;">
                                                <p class="mt-4"> <b>Species:</b> {{x.species}}</p>
                                            </div>
                                            <div style="margin-top: -20px; font-weight: bold; font-style: italic; font-family: 'Courier New', Courier, monospace;">
                                                <p class="mt-4"> <b>Status:</b> {{x.status}}</p>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div v-if="validation == '0'" class="row col-12">
                            <div class="row col-12" style="margin-bottom: 10px; margin-top: 20px;">
                                <div class="row col-4"></div>
                                <div class="row col-4">
                                    <button @click="set_characters()" type="button" class="btn btn-primary">Characters</button>
                                </div>
                                <div class="row col-4"></div>
                            </div>
                            <div v-for="e in episodes" style="margin-top: 5%;" class="col-6 mt-4 d-flex justify-content-center">
                                <div class="col-sm-12 col-md-12">
                                    <div id="card" style="background-color: white;" class="card">
                                        <div  class="card-body row">
                                            <div style="font-weight: bold; font-style: italic; font-family: 'Courier New', Courier, monospace;" class="text-center"><b>{{e.name}}</b></div>
                                            <div style="margin-top: -20px; font-weight: bold; font-style: italic; font-family: 'Courier New', Courier, monospace;">
                                                <p class="mt-4"> <b>link episode: </b><a :href="e.url">{{e.url}}</a></p>
                                            </div>
                                            <div style="margin-top: -20px; font-weight: bold; font-style: italic; font-family: 'Courier New', Courier, monospace;">
                                                <p class="mt-4"> <b>Episode Date:</b> {{e.air_date}}</p>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default{
        data: function () {
            return {
                api: null,
                episodes: null,
                validation: '1',
                modal: false
            }
        },
        computed: {
        },
        methods: {
            set_episodes(){
                this.get_episodes();
                this.validation = '0';
            },
            set_characters(){
                this.get_api();
                this.validation = '1';
            },
            get_api(){
                fetch("https://rickandmortyapi.com/api/character").then(res => { res.json().then((x) =>{this.api = x.results})})
            },
            get_episodes(){
                fetch("https://rickandmortyapi.com/api/episode").then(res => { res.json().then((x) =>{this.episodes = x.results})})
            },
        },
        mounted: function () {
            this.get_api();
        }
    }
</script>

<style scoped>
</style>