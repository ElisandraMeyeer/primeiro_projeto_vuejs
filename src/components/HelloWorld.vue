<script>
export default {
  data() {
    return {
      inputTipoPao: "",
      inputSalada: [],
      inputMolhos: [],
      inputHamburguer: "",
      etapa: 1,
      inputNome: "",
      inputEndereco: "",
      novoPedidoAssincrono: null
    };
  },

  methods: {},
  computed: {
    pao() {
      switch (this.inputTipoPao) {
        case "gergelim":
          return ["/pao_gergelim_superior.png", "/pao_gergelim_inferior.png"];
        case "australiano":
          return [
            "/pao_australiano_superior.png",
            "/pao_australiano_inferior.png",
          ];
        default:
          return ["/padrao/pao_superior.png", "/padrao/pao_inferior.png"];
      }
    },
    alface() {
      if (this.inputSalada.includes("alface")) {
        return "/alface.png";
      } else {
        return "/padrao/alface.png";
      }
    },
    ketchup() {
      if (this.inputMolhos.includes("ketchup")) {
        return "/ketchup.png";
      } else {
        return "/padrao/molho.png";
      }
    },
    maionese() {
      if (this.inputMolhos.includes("maionese")) {
        return "/maionese.png";
      } else {
        return "/padrao/molho.png";
      }
    },
    mostarda() {
      if (this.inputMolhos.includes("mostarda")) {
        return "/mostarda.png";
      } else {
        return "/padrao/molho.png";
      }
    },
    hamburguer() {
      switch (this.inputHamburguer) {
        case "bovino":
          return ["/bovino.png"];
        case "frango":
          return ["/frango.png"];
        case "soja":
          return ["/soja.png"];
        default:
          return ["/padrao/hamburguer.png"];
      }
    },

    fazerPedido() {
      if (this.inputTipoPao && this.inputHamburguer) {
        this.etapa = 2;
      } else {
        alert(
          "Você precisa selecionar pelo menos um tipo de pão e um tipo de hamburguer"
        );
      }
    },
    confirmarPedido() {
      if (this.inputNome && this.inputEndereco) {
        this.etapa = 3;

        this.novoPedidoAssincrono = setTimeout(() => this.novoPedido(), 7000);
      } else {
        alert("Você precisa informar seu nome e endereço");
      }
    },

    novoPedido() {
      this.etapa = 1;

      this.inputTipoPao = "";
      this.inputSalada = [];
      this.inputMolhos = [];
      this.inputHamburguer = "";
      this.inputNome = "";
      this.inputEndereco = "";
    },
  },
  watch: {
    etapa(novoValor){
      if(novoValor == 1){
        clearTimeout(this.novoPedidoAssincrono)
      }

    }
  },
};
</script>

<template>
  <nav class="navbar bg-light">
    <div class="container">
      <span class="navbar-brand mb-0 h1">Monte o seu Lanche</span>
    </div>
  </nav>

  <div class="container">
    <div class="row">
      <div class="col-md-6">
        <div class="row mt-2">
          <div class="col">
            <img :src="pao[0]" />
            <img :src="alface" />
            <img :src="ketchup" />
            <img :src="maionese" />
            <img :src="mostarda" />
            <img :src="hamburguer" />
            <img :src="pao[1]" />
          </div>
        </div>
      </div>
      <div class="col-md-6" v-if="etapa == 1">
        <!-- TIPO DO PÃO -->
        <div class="row">
          <div class="col">
            <div class="card">
              <div class="card-header">TIPO DO PÃO</div>
              <div class="card-body">
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    value="gergelim"
                    v-model="inputTipoPao"
                  />
                  <label class="form-check-label">Gergelim</label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    value="australiano"
                    v-model="inputTipoPao"
                  />
                  <label class="form-check-label"> Australiano </label>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- SALADAS -->
        <div class="row mt-2">
          <div class="col">
            <div class="card">
              <div class="card-header">SALADAS</div>
              <div class="card-body">
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    value="alface"
                    v-model="inputSalada"
                  />
                  <label class="form-check-label"> Alface </label>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- MOLHOS -->
        <div class="row mt-2">
          <div class="col">
            <div class="card">
              <div class="card-header">MOLHOS</div>
              <div class="card-body">
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    value="ketchup"
                    v-model="inputMolhos"
                  />
                  <label class="form-check-label"> Ketchup </label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    value="mostarda"
                    v-model="inputMolhos"
                  />
                  <label class="form-check-label"> Mostarda </label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="checkbox"
                    value="maionese"
                    v-model="inputMolhos"
                  />
                  <label class="form-check-label"> Maionese </label>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- TIPO HAMBURGUER -->
        <div class="row mt-2">
          <div class="col">
            <div class="card">
              <div class="card-header">TIPO DE HAMBÚRGUER</div>
              <div class="card-body">
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    value="bovino"
                    v-model="inputHamburguer"
                  />
                  <label class="form-check-label"> Bovino </label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    value="frango"
                    v-model="inputHamburguer"
                  />
                  <label class="form-check-label"> Frango </label>
                </div>
                <div class="form-check form-check-inline">
                  <input
                    class="form-check-input"
                    type="radio"
                    value="soja"
                    v-model="inputHamburguer"
                  />
                  <label class="form-check-label"> Soja </label>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="row mt-02">
          <div class="col d-flex justify-content-end">
            <button
              type="button"
              class="btn btn-primary"
              @click="fazerPedido()"
            >
              Fazer pedido
            </button>
          </div>
        </div>
      </div>

      <div class="col-md-6" v-if="etapa == 2">
        <div class="row mt-2">
          <div class="col">
            <div class="card">
              <div class="card-header">INFORME SEUS DADOS</div>
              <div class="card-body">
                <div class="mb-3">
                  <label class="form-label">Nome</label>
                  <input type="text" class="form-control" v-model="inputNome" />
                </div>
                <div class="mb-3">
                  <label class="form-label">Endereço</label>
                  <input
                    type="text"
                    class="form-control"
                    v-model="inputEndereco"
                  />
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="row mt-2">
          <div class="col d-flex justify-content-between">
            <button type="button" class="btn btn-warning" @click="etapa -= 1">
              Voltar
            </button>
            <button
              type="button"
              class="btn btn-success"
              @click="confirmarPedido()"
            >
              Confirmar
            </button>
          </div>
        </div>
      </div>

      <div class="col-md-6" v-if="etapa == 3">
        <div class="row mt-2">
          <div class="col">
            <div class="card">
              <div class="card-header">PEDIDO CONFIRMADO</div>
              <div class="card-body"><p>Aguarde seu pedido</p></div>
            </div>
          </div>

          <div class="row mt-2">
            <div class="col d-flex justify-content-between">
              <button type="button" class="btn btn-primary" @click="etapa = 1">
                Repetir pedido
              </button>
              <button type="button" class="btn btn-success" @click="novoPedido">
                Novo pedido
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>



<style scoped>
</style>
