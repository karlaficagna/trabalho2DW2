<template>
  <div class="produto-detalhe">
    <Header />
    <section>
      <div class="container">
        <div class="row">
          <div class="col-md-12">
            <h2>{{ produtoDetalhe.title }}</h2>
            <img :src="produtoDetalhe.img" />
          </div>
        </div>
      </div>
    </section>
    <main>
      <Detalhe />
    </main>
    <Footer />
  </div>
</template>
<script>
import Header from "../components/Header.vue";
import Detalhe from "../components/Detalhe.vue";
import Footer from "../components/Footer.vue";

export default {
  name: "ProdutoDetalhe",
  components: {
    Header,
    Detalhe,
    Footer,
  },
  data: function () {
    return {
      produtoDetalhe: {},
    };
  },
  methods: {
    getProdByID: async function () {
      const result = await fetch(
        "http://localhost:3000/produtos/" + this.$route.params.id
      )
        .then((res) => res.json())
        .catch((error) => {
          return {
            error: true,
            message: error,
          };
        });
      if (!result.error) {
        this.produtoDetalhe = result;
      }
    },
  },
  created: function () {
    this.getProdByID();
  },
};
</script>
<style>
</style>