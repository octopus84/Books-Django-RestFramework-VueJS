<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col text-left">
                <h2>
                    Nuevo Libro
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
                                        <b-button type="submit" variant="success">Crear</b-button>
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
            // bookId: this.$route.params.bookId,
            form: {
                title: '',
                description: '',
            },
        }
    },
    methods: {
        onSubmit(event) {
            event.preventDefault()
            const path = `http://127.0.0.1:8000/api/v1.0/books/`

            axios.post(path, this.form).then((response) => {
                this.form.title = response.data.title
                this.form.description = response.data.description
                // alert('Libro actualizado exitosamente!')
                swal('Libro creado exitosamente!', "","success")
            }).catch((error) => {
                console.log(error)
                swal('El libro no ha sido creado!', "","error")
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
        // this.getBook()
    },
}
</script>

<style lang="css" scoped>

</style>