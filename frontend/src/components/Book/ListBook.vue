<template>
    <div class="container">
        <div class="row">
            <div class="col text-left">
                <h2>Listado de Libros</h2>
                <b-button size="sm" :to="{name: 'NewBook'}" variant="success">
                    Nuevo Libro
                </b-button>
                <div class="col-md-12">
                    <b-table striped hover :items="books" :fields="fields">

                        <template v-slot:cell(action)="{ item }">
                            <span>
                                <!-- <b-btn @click="(item)" variant="primary" >Editar</b-btn> -->
                                <b-btn variant="primary" :to="{  name:'EditBook', params: {bookId: item.id} }">Editar
                                </b-btn>
                            </span>
                            <span>
                                <b-btn variant="danger" :to="{  name:'DeleteBook', params: {bookId: item.id} }">Eliminar
                                </b-btn>
                            </span>
                        </template>

                    </b-table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            fields: [
                { key: 'id', label: 'Id' },
                { key: 'title', label: 'Titulo' },
                { key: 'description', label: 'Decripcion' },
                { key: 'action', label: 'Actión' },
            ],
            books: []
        }
    },
    methods: {
        getBooks() {
            const path = 'http://127.0.0.1:8000/api/v1.0/books/'
            console.log('log: ' + path)
            axios.get(path).then((response) => {
                this.books = response.data
            }).catch((error) => {
                console.log(error)
            })
        }
    },
    created() {
        this.getBooks()
    },
}
</script>

<style lang="css" scoped>

</style>