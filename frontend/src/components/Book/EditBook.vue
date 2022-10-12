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
                        <form @onSubmit="onSubmit">
                            <div class="form-group row">
                                <label for="title" class="col-sm-2 col-form-label">Título</label>
                                <div class="col-sm-6">
                                    <input type="text" placeholder="Título" name="title" class="form-control">
                                </div>
                            </div>
                            <div class="form-group row">
                                <label for="description" class="col-sm-2 col-form-label">Descripción</label>
                                <div class="col-sm-6">
                                    <textarea placeholder="Descripción" name="description" class="form-control"
                                        cols="30" rows="10">

                                    </textarea>
                                </div>
                            </div>
                            <div class="rows">
                                <div class="col text-left">
                                    <span>
                                        <b-btn type="submit" size="lg" variant="primary">Editar</b-btn>
                                    </span>
                                    <span>
                                        <b-btn type="submit" size="lg" variant="danger" :to="{ name: 'ListBook'} ">Cancelar</b-btn>
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
export default {

}
</script>
<style lang="css" scoped>

</style>