<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col text-left">
                <h2>
                    Editar Libro
                </h2>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <div class="card">
                    <div class="card-body">
                        <form @submit="onSubmit" @cancel="onCancel">
                            <div class="form-group row">
                                <label for="title" class="col-sm-2 col-form-label">Título</label>
                                <div class="col-sm-6">
                                    <input type="text" placeholder="Título" name="title" class="form-control"
                                        v-model.trim="form.title">
                                </div>
                            </div>
                            <div class="form-group row">
                                <label for="description" class="col-sm-2 col-form-label">Descripción</label>
                                <div class="col-sm-6">
                                    <textarea placeholder="Descripción" name="description" class="form-control"
                                        v-model.trim="form.description" cols="30" rows="10">

                                    </textarea>
                                </div>
                            </div>
                            <div class="rows">
                                <div class="col text-left">
                                    <span>
                                        <b-button type="submit" variant="primary">Editar</b-button>
                                    </span>
                                    <span>
                                        <b-button type="submit" variant="danger" :to="{ name: 'ListBook'} ">
                                            Cancelar</b-button>
                                    </span>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import swal from 'sweetalert'

export default {
    data() {
        return {
            bookId: this.$route.params.bookId,
            form: {
                title: 'default title',
                description: 'default  descripcion',
            },
        }
    },
    methods: {
        onSubmit(event) {
            event.preventDefault()
            const path = `http://127.0.0.1:8000/api/v1.0/books/${this.bookId}/`

            axios.put(path, this.form).then((response) => {
                this.form.title = response.data.title
                this.form.description = response.data.description
                // alert('Libro actualizado exitosamente!')
                swal('Libro actualizado exitosamente!')
            }).catch((error) => {
                console.log(error)
            })

        },
        getBook() {
            const path = `http://127.0.0.1:8000/api/v1.0/books/${this.bookId}/`
            // console.log('log:' + path)

            axios.get(path).then((response) => {
                this.form.title = response.data.title
                this.form.description = response.data.description
            }).catch((error) => {
                console.log(error)
            })
        },
        onCancel(event) {
            event.preventDefault()
            // Reset our form values
            this.form.title = ''
            this.form.description = ''
        },
    },
    created() {
        this.getBook()
    },
}
</script>

<style lang="css" scoped>

</style>