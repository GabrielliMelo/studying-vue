<template>
  <div class="painel">
    <p>{{ texto }}</p>
    <h2 class="painel-titulo" @click="visivel = !visivel">
      {{ titulo }}
    </h2>
    <transition name="painel-fade">
      <div class="painel-conteudo" v-show="visivel">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: ["titulo", "texto"],
  data() {
    return {
      visivel: true
    };
  }
};
</script>

<style scoped>
.painel {
  padding: 0 auto;
  border: solid 2px grey;
  display: inline-block;
  margin: 5px;
  box-shadow: 5px 5px 10px grey;
  width: 200px;
  height: 100%;
  vertical-align: top;
  text-align: center;
}

.painel .painel-titulo {
  text-align: center;
  border: solid 2px;
  background: lightblue;
  margin: 0 0 15px 0;
  padding: 10px;
  text-transform: uppercase;
}
* {
  box-shadow: 3px 3px 5px rgb(22, 22, 22);
}
.painel-conteudo {
  overflow: hidden;
}
.painel-fade-enter,
.painel-fade-leave-active {
  opacity: 0;
}
.painel-fade-enter-active,
.painel-fade-leave-active {
  transition: opacity 1s;
}
</style>
