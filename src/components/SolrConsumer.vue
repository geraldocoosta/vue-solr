<template>
  <div>
    <nav class="navbar navbar-light bg-light">
      <span class="navbar-brand mb-0 h1">Consumido solr</span>
    </nav>
    <div class="container">
      <div class="form-group">
        <label for="busca-solr">Busca</label>
        <input
          type="text"
          class="form-control"
          id="busca-solr"
          aria-describedby="desc-busca-solr"
          placeholder="Entre com a pesquisa"
          @keypress="pesquisarCampos" />
        <small id="desc-busca-solr"
          class="form-text text-muted" >Insira dados para pesquisar com no SOLR</small>
      </div>
      <div class="resultados">
          <div class="card" v-for="item in itens.docs" :key="item.id">
            <div class="card-body">
              <div class="card-header">
               <h5 class="card-title">{{item.causa_acidente}}</h5>
              </div>
              <p class="card-text">BR: <span class="float-right">{{item.br}}</span></p>
              <p class="card-text">data acidente: <span class="float-right">{{item.data_acidente}}</span></p>
              <p class="card-text">dia semana: <span class="float-right">{{item.dia_semana}}</span></p>
              <p class="card-text">uf: <span class="float-right">{{item.uf}}</span></p>
              <p class="card-text">classificacao acidente: <span class="float-right">{{item.classificacao_acidente}}</span></p>
              <p class="card-text">mortos: <span class="float-right">{{item.mortos}}</span></p>
              <p class="card-text">feridos leves: <span class="float-right">{{item.feridos_leves}}</span></p>
              <p class="card-text">feridos graves: <span class="float-right">{{item.feridos_graves}}</span></p>
              <p class="card-text">ilesos: <span class="float-right">{{item.ilesos}}</span></p>
              <p class="card-text">MUNICIPIO: <span class="float-right">{{item.municipio}}</span></p>
            </div>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {

  data: function() {
    return {
      pesquisa: "",
      itens: {}
    };
  },
  methods: {
    pesquisarCampos: function(event) {
      axios.get(`http://localhost:8983/solr/acidentes/select?indent=off&q=${event.target.value}&wt=json`)
        .then(response => response.data)
        .then(data => this.itens = data.response);
    }
  }
};
</script>
