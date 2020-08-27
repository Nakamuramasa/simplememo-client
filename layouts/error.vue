<template>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <div class="card mt-3">
                    <div class="card-body pt-0">
                        <div class="card-text">

                            <section class="authentication">
                                <div class="auth-body text-center">
                                    <h1 class="text-uppercase fw-500 mb-4 text-center font-22">
                                        <i class="fas fa-exclamation-triangle"></i>
                                        ERROR {{ error.statusCode }}
                                    </h1>
                                    <p>{{ error.message }}</p>
                                    <p class="linkToTop font-20 fw-400 text-center mt-4">
                                        <nuxt-link to="/">Top page</nuxt-link>
                                    </p>
                                </div>
                            </section>

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['error']
};
</script>
