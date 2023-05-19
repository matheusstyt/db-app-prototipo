<template>
  <div class="container-nova-receita">
    <h2> Receita: {{ receita_nome }} </h2>
    <div class="input-field">
        <label for="">Nome da receita</label>
        <input type="text" placeholder="Ex: Pão Frances.." v-model="receita_nome">
      </div>
      <div class="container-base"> 
        <h3>Ingrediente Base</h3>
        <div>
        <div class="input-field">
            <label for="">Nome</label>
            <input type="text" placeholder="Ex: Farinha.." v-model="ingrediente_base_nome">
        </div>
        <div class="input-field">
            <label for="">Peso ( g / ml )</label>
            <input type="number" placeholder="Ex: 5000" v-model="ingrediente_base_peso">
        </div>
        </div>
      </div>
    
    <form @submit="adicionar_receita">
      <h3>Novo Ingrediente</h3>
      <div class="input-field">
        <label for="">Nome</label>
        <input type="text" placeholder="Ex: Farinha.." v-model="ingrediente_novo_nome">
      </div>
      <div class="input-field">
        <label for="">Porcentagem</label>
        <input type="number" placeholder="Ex: 10" v-model="ingrediente_novo_porcentagem">
      </div>
      <div class="input-field">
        <label for="">Unidade</label>
        <select name="" id="" v-model="ingrediente_novo_unidade">
          <option value="g">g</option>
          <option value="ml">ml</option>
        </select>
      </div>
    </form>
    <button @click="adicionar_receita">+</button>
    <ul>
      <template v-for="(ingrediente, index) in list_ingredientes">
        <li>
          <p>{{ ingrediente.nome }}</p>
          <p>{{ ingrediente.porcentagem }}</p>
          <p>{{ ingrediente.peso }}</p>
        </li>
      </template><li>

      </li>
    </ul>
    <button @click="salvar_receita">Salvar</button>
  </div>
</template>
<script>
export default {
    data(){
        return{
            receita_nome : null,
            list_ingredientes : [],
            ingrediente_base_nome : null,
            ingrediente_base_peso : null,

            ingrediente_novo_nome : null,
            ingrediente_novo_porcentagem : null,
            ingrediente_novo_unidade : null,
        }
    },
    methods : {
        regra_tres(porcentagem_novo, peso_base){
        return (peso_base * porcentagem_novo) / 100;
        },
        adicionar_receita(e){
        const novo_ingrediente = {
            nome : this.ingrediente_novo_nome,
            porcentagem : this.ingrediente_novo_porcentagem,
            peso : this.ingrediente_base_peso 
            ? `${this.regra_tres(this.ingrediente_base_peso, this.ingrediente_novo_porcentagem)}${this.ingrediente_novo_unidade}` 
            : `0${this.ingrediente_novo_unidade}`
        }
        this.list_ingredientes.push(novo_ingrediente);
        e.preventDefault();
        
        },
        salvar_receita(){
            const receita = {
                receita_nome : this.receita_nome,
                base : {
                    nome : this.ingrediente_base_nome,
                    peso : this.ingrediente_base_peso
                },
                ingredientes : this.list_ingredientes
            }
            console.log(receita);
        }
    },
    watch : {
        ingrediente_base_peso(value){
        console.log(value)
        },

    }
}
</script>